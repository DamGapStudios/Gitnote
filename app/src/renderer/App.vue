<template xmlns:v-badge="http://www.w3.org/1999/xhtml">
  <div id="#app">
    <v-app id="example-1">
      <v-toolbar>
        <v-toolbar-title>
          GitNote
        </v-toolbar-title>
      </v-toolbar>
      <main>
        <v-content>
          <v-container fluid class="container">
            <router-view></router-view>
          </v-container>
        </v-content>
      </main>
      <v-footer>Copyright <i class="fa fa-copyright" aria-hidden="true"></i> <span v-model="year"></span> DamGap Studios</v-footer>
    </v-app>
  </div>
</template>

<script>
  import store from 'renderer/vuex/store';
  export default {
    data() {
      return {
        year: new Date().getFullYear(),
        repos: [],
      };
    },
    store,
  };
</script>

<style lang="stylus">
  @import 'stylus/main'
  @import url(https://fonts.googleapis.com/css?family=Lato:300);

    .container {
        padding 10px
    }
</style>
