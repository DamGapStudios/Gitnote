<template xmlns:v-badge="http://www.w3.org/1999/xhtml">
  <div id="#app">
    <v-app id="example-1">
      <v-toolbar>
        <v-toolbar-title>
          <span  v-badge:1.overlap class="green--after">GitNot</span>
        </v-toolbar-title>
      </v-toolbar>
      <main>
        <v-content>
          <v-container fluid>
            <router-view></router-view>
          </v-container>
        </v-content>
      </main>
      <v-footer>Footer</v-footer>
    </v-app>
  </div>
</template>

<script>
  import store from 'renderer/vuex/store';
  export default {
    store,
  };
</script>

<style lang="stylus">
  @import 'stylus/main'
  @import url(https://fonts.googleapis.com/css?family=Lato:300);
  @import url(https://fonts.googleapis.com/css?family=Roboto:Material+Icons);
  @import url(https://unpkg.com/vuetify/dist/vuetify.min.css);
</style>
