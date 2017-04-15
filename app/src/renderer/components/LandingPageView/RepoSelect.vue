<template xmlns:v-badge="http://www.w3.org/1999/xhtml">
    <div>
        <v-row>
            <v-col xs9>
                <v-text-field
                        label="Repo URL"
                        v-model='repoURL'
                ></v-text-field>
            </v-col>
            <v-col xs3>
                <v-btn light flat @click.native="saveLink()">Add Repo</v-btn>
            </v-col>
        </v-row>
    </div>
</template>

<script>
    import store from 'renderer/vuex/store';
    export default {
      data() {
        return {
          repoName: 'GitNote',
          repoAuthor: 'Adrian Dunham, Anthony Garera',
          repoURL: 'https://github.com/DamGapStudios/Gitnote',
          repoDescription: 'A project to notify you when someone pushed something to a repo',
        };
      },
      store,
      methods: {
        saveLink() {
// eslint-disable-next-line no-console
          console.log(this.repoURL);
        },
      },
    };
</script>

<style lang="stylus">

</style>
