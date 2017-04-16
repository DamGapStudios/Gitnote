<template xmlns:v-badge="http://www.w3.org/1999/xhtml">
    <div>
        <v-card class="padding">
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
                <h5>{{ repoOwner }}</h5>
                <i class="fa fa-star yellow--text" aria-hidden="true"></i>{{ repoStars }}
                <i class="fa fa-star yellow--text" aria-hidden="true"></i>{{ repoIssues }}
            </v-card-text>
            <v-card-row actions>
                <v-btn flat class="green--text darken-1" :href='repoURL'>View Repo</v-btn>
            </v-card-row>
        </v-card>
    </div>
</template>

<script>
    import store from 'renderer/vuex/store';
    export default {
      props: ['repoName', 'repoOwner', 'repoURL', 'repoStars', 'repoIssues'],
      store,
    };
</script>

<style lang="stylus">
    .padding{
        padding-bottom 10px
    }
</style>
