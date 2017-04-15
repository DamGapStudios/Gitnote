<template xmlns:v-badge="http://www.w3.org/1999/xhtml">
    <v-card>
        <v-card-row class="green darken-1">
            <v-card-title>
                <span class="white--text">{{ repoName }}</span>
                <v-spacer></v-spacer>
                <div>
                    <v-menu id="repoActions" bottom left origin="top right">
                        <v-btn icon="icon" slot="activator" class="white--text">
                            <i class="fa fa-ellipsis-v fa-2x" aria-hidden="true"></i>
                        </v-btn>
                        <v-list>
                            <v-list-item>
                                <v-list-tile>
                                    <v-list-tile-title>Remove Card</v-list-tile-title>
                                </v-list-tile>
                            </v-list-item>
                            <v-list-item>
                                <v-list-tile>
                                    <v-list-tile-title>Send Feedback</v-list-tile-title>
                                </v-list-tile>
                            </v-list-item>
                        </v-list>
                    </v-menu>
                </div>
            </v-card-title>
        </v-card-row>
        <v-card-text>
            <h5>{{ repoAuthor }}</h5>
        </v-card-text>
        <v-card-row actions>
            <v-btn flat class="green--text darken-1" :href='repoURL'>View Repo</v-btn>
        </v-card-row>
    </v-card>
</template>

<script>
    import store from 'renderer/vuex/store';
    export default {
      data() {
        return {
          repoName: 'GitNote',
          repoAuthor: 'DamGapStudios',
          repoURL: 'https://github.com/DamGapStudios/Gitnote',
          repoDescription: 'A project to notify you when someone pushed something to a repo',
        };
      },
      store,
    };
</script>

<style lang="stylus">

</style>
