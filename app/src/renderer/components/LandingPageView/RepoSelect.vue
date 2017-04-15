<template xmlns:v-badge="http://www.w3.org/1999/xhtml">
    <div>
        <v-row>
            <v-col xs5>
                <v-text-field
                        label="Repo Author"
                        v-model='repoAuthor'
                ></v-text-field>
            </v-col>
            <v-col xs5>
                <v-text-field
                        label="Repo Name"
                        v-model='repoName'
                ></v-text-field>
            </v-col>
            <v-col xs2>
                <v-btn light flat @click.native="saveLink(repoAuthor, repoName)">Add Repo</v-btn>
            </v-col>
        </v-row>
    </div>
</template>

<script>
    /* eslint-disable no-console */

    import store from 'renderer/vuex/store';
    export default {
      data() {
        return {
          repoName: 'GitNote',
          repoAuthor: 'DamGapStudios',
          repoURL: 'DamGapStudios/Gitnote',
          repoDescription: 'A project to notify you when someone pushed something to a repo',
        };
      },
      store,
      methods: {
        saveLink(repoAuthor, repoName) {
// eslint-disable-next-line no-console
          console.log(repoAuthor, repoName);
          // GET /someUrl
          this.$http.get(`https://api.github.com/repos/${repoAuthor}/${repoName}`).then(response => {
            // get body data
            this.someData = response.body;
            console.log(this.someData);
          },
          response => {
             // error callback
// eslint-disable-next-line indent
            console.log(response);
          });
        },
      },
    };
</script>

<style lang="stylus">

</style>
