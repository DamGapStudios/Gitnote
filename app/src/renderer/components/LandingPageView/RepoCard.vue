<template xmlns:v-badge="http://www.w3.org/1999/xhtml">
    <div>
        <v-card class="padding">
            <v-card-row class="green darken-1">
                <v-card-title>
                    <span class="white--text">{{ repo.name }}</span>
                    <v-spacer></v-spacer>
                    <div>
                        <v-menu id="repoActions" bottom left origin="top right">
                            <v-btn icon="icon" slot="activator" class="white--text">
                                <i class="fa fa-ellipsis-v fa-2x" aria-hidden="true"></i>
                            </v-btn>
                            <v-list>
                                <v-list-item>
                                    <v-list-tile>
                                        <v-list-tile-title><i class="fa fa-trash" aria-hidden="true"></i> Remove Card</v-list-tile-title>
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
                <h5>{{ repo.owner.login }}</h5>
                <i class="fa fa-star yellow--text" aria-hidden="true"></i>{{ repo.stargazers_count }}
                <i class="fa fa-exclamation-triangle red--text" aria-hidden="true"></i>{{ repo.open_issues}}
            </v-card-text>
            <v-card-row actions>
                <v-btn flat class="green--text darken-1" :href='repo.html_url'>View Repo</v-btn>
                <v-btn flat class="green--text darken-1" @click.native='sendNotification(repo.name,`${repo.name} by ${repo.owner.login}`)'>Send Notification</v-btn>
            </v-card-row>
        </v-card>
    </div>
</template>

<script>
    import store from 'renderer/vuex/store';
    export default {
      props: ['repo'],
      store,
      mounted() {
// eslint-disable-next-line no-console
        console.log(this.repo);
      },
      created() {
        this.getCommits(this.repo.name, this.repo.commits_url);
        this.dateMinusOne();
      },
      methods: {
        getCommits(name, commitURL) {
// eslint-disable-next-line no-console
          console.log(name, commitURL);
          this.$http.get(`${commitURL}?since=${this.dateMinusOne()}`).then(response => {
            this.data = response.body[0];
// eslint-disable-next-line no-console
            console.log(this.data);
            if (this.data === undefined) {
              this.sendNotification(
                name,
                'No New pushes'
              );
            } else {
              this.sendNotification(
                name,
                `${this.data.commit.committer.name} pushed ${this.data.commit.message}`
              );
            }
          },
            response => {
              // error callback
// eslint-disable-next-line no-console
              console.log(response);
            });
        },
        sendNotification(name, message) {
// eslint-disable-next-line no-console
          console.log(name, message);
          const myNotification = new Notification(name, {
            body: message,
          });

          myNotification.onclick = () => {
// eslint-disable-next-line no-console
            console.log('Notification clicked');
          };
        },
        dateMinusOne() {
          this.currentDate = new Date();
          this.minusMinute = new Date(this.currentDate - (1000 * 60)).toISOString();
          return this.minusMinute;
        },
      },
    };
</script>

<style lang="stylus">
    .padding{
        margin-bottom 10px
    }
</style>
