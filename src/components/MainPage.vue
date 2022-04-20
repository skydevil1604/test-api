<template>
  <div>
    <md-app md-mode="reveal">
      <md-app-toolbar class="md-primary">
        <!-- <md-button class="md-icon-button" @click="menuVisible = !menuVisible">
          <md-icon>menu</md-icon>
        </md-button> -->
        <span class="md-title">Main Page</span>
      </md-app-toolbar>

      <!-- <md-app-drawer :md-active.sync="menuVisible">
        <md-toolbar class="md-transparent" md-elevation="0">Navigation</md-toolbar>

        <md-list>
          <md-list-item>
            <md-icon>move_to_inbox</md-icon>
            <span class="md-list-item-text">Inbox</span>
          </md-list-item>

          <md-list-item>
            <md-icon>send</md-icon>
            <span class="md-list-item-text">Sent Mail</span>
          </md-list-item>

          <md-list-item>
            <md-icon>delete</md-icon>
            <span class="md-list-item-text">Trash</span>
          </md-list-item>

          <md-list-item>
            <md-icon>error</md-icon>
            <span class="md-list-item-text">Spam</span>
          </md-list-item>
        </md-list>
      </md-app-drawer> -->

      <md-app-content>
        <div class="item" v-for="item in data" :key="item.id">
          <p class="hash">{{ item.hash }}:</p>
          <div v-if="item.content.length > 1">
            <p  class="content"
                v-for="(elem, index) in item.content"
                :key="index"
            >{{ elem }}</p>
          </div>
          <div v-else>
            <p class="content">{{ item.content[0] }}</p>
          </div>
        </div>
      </md-app-content>
    </md-app>
    <md-field>
      <label>Textarea</label>
      <md-textarea v-model="textarea"></md-textarea>
    </md-field>
    <md-button @click="onPostButtonClick" class="md-primary md-raised">POST</md-button>
  </div>
</template>

<script>
export default {
  name: 'MainPage',
  props: {
    data: Array,
    default: () => ([])
  },
  data: () => ({
    // menuVisible: false
    textarea: '',
  }),
  methods: {
    onPostButtonClick() {
      if(this.textarea) {
        this.$emit("onPostButtonClick", {
          id: Math.round(Math.random() * 100),
          hash: `HASH${Math.round(Math.random() * 100)}`,
          content: [this.textarea]
        });
        this.textarea = ''
      } else {
        alert('Type content!')
      }
    }
  }
}
</script>

<style scoped lang="scss">
.md-app {
    max-height: 1000px;
    border: 1px solid rgba(#000, .12);
  }

   // Demo purposes only
  .md-drawer {
    width: 230px;
    max-width: calc(100vw - 125px);
  }

  .item {
    display: flex;
    justify-content: center;

    .content {
      margin-left: 50px;
    }
  }
</style>
