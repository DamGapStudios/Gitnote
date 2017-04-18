<template>
  <div>
    <h1 class="center code-words">Welcome</h1>
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
    <h3 class="center"> Repos</h3>
      <RepoCard v-for="repo in repos" :repo='repo.value'></RepoCard>
  </div>
</template>

<script>
  import RepoCard from './LandingPageView/RepoCard.vue';
  import RepoSelect from './LandingPageView/RepoSelect.vue';
  export default {
    mounted() {
      this.$iterateStorage((value, key) => {
        this.currentDate = new Date();
        this.minusMinute = new Date(this.currentDate - (1000 * 60)).toISOString();
// eslint-disable-next-line no-console
        console.log(this.minusMinute);
        this.repos.push({ key, value });
//          console.log all the kay/value pairs
// eslint-disable-next-line no-console
        console.log(this.repos);
      }, err => {
        if (!err) {
// eslint-disable-next-line no-console
          console.log('Iteration has completed');
        }
      });
    },
    created() {
//      this.currentDate = new Date();
//      this.minusMinute = new Date(this.currentDate - (1000 * 60)).toISOString();
//      this.notifications(this.minusMinute);
    },
    components: {
      RepoCard,
      RepoSelect,
    },
    data() {
      return {
        repos: [],
        repoName: 'GitNote',
        repoAuthor: 'DamGapStudios',
        repoURL: 'DamGapStudios/Gitnote',
        repoDescription: 'A project to notify you when someone pushed something to a repo',
      };
    },
    name: 'landing-page',
    methods: {
      saveLink(repoAuthor, repoName) {
// eslint-disable-next-line no-console
        console.log(repoAuthor, repoName);
              // GET /someUrl
        this.$http.get(`https://api.github.com/repos/${repoAuthor}/${repoName}`).then(response => {
                // get body data
          this.someData = response.body;
// eslint-disable-next-line no-console
          console.log(this.someData);
          const id = this.someData.id;
          const data = this.someData;
          const name = this.someData.name;
          this.$setItem(id, data);
          const myNotification = new Notification('GitNot', {
            body: `${name} repo added`,
          });
          myNotification.onclick = () => {
// eslint-disable-next-line no-console
            console.log('Notification clicked');
          };
          this.repos.push({ key: id, value: data });
// eslint-disable-next-line no-console
          console.log(this.repos);
        },
        response => {
                // error callback
// eslint-disable-next-line no-console
          console.log(response);
        });
      },
      notifications(currentTime) {
        this.$http.get(`https://api.github.com/repos/DamGapStudios/GitNote/commits?since${currentTime}`).then(response => {
          this.someData = response.body;
          this.date = new Date();
// eslint-disable-next-line no-console
          console.log(this.date - (1000 * 60));
          const author = this.someData;
          const myNotification = new Notification('GitNote', {
            body: `${author} updated`,
          });
          this.currentDate = new Date();
          this.minusMinute = new Date(this.currentDate - (1000 * 60)).toISOString();
          setTimeout(this.notifications(this.minusMinute), 60000);
          myNotification.onclick = () => {
// eslint-disable-next-line no-console
            console.log('Notification clicked');
          };
        });
      },
    },
  };
</script>

<style scoped>
  img {
    margin-top: -25px;
    width: 450px;
  }

  .center {
    text-align: center;
  }

  .code-words {
      font-family:	Courier New, monospace;
  }

</style>
