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
      <RepoCard v-for="repo in repos" :repo-name='repo.value.name' :repo-owner='repo.value.owner.login' :repo-url="repo.value.svu_url" :repo-stars="repo.value.stargazers_count" :repo-issues="repo.value.open_issues"></RepoCard>
  </div>
</template>

<script>
  import RepoCard from './LandingPageView/RepoCard.vue';
  import RepoSelect from './LandingPageView/RepoSelect.vue';
  export default {
    mounted() {
      this.$iterateStorage((value, key) => {
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
          this.$setItem(id, data);
          this.repos.push({ id, data });
        },
        response => {
                // error callback
// eslint-disable-next-line no-console
          console.log(response);
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
