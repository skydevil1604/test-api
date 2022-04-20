<template>
  <div id="app">
    <section v-if="errored">
      <p>We're sorry, we're not able to retrieve this information at the moment, please try back later</p>
    </section>
    <section v-else>
      <div v-if="loading">Loading...</div>
      <div v-else>
        <MainPage :data="data" @onPostButtonClick="handlerPost"/>
      </div>
    </section>
  </div>
</template>

<script>
import MainPage from './components/MainPage.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    MainPage
  },
  data: () => ({
    data: [],
    loading: true,
    errored: false
  }),
  mounted() {
    axios
      .get('http://localhost:3000/hash')
      .then(response => {
        this.data = response.data;
      })
      .catch(error => {
        console.log(error);
        this.errored = true;
      })
      .finally(() => (this.loading = false));
  },
  methods: {
    handlerPost(post) {
      axios
        .post('http://localhost:3000/hash', post);
        this.data.push(post)

    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
