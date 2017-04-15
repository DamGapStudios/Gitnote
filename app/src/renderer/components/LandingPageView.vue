<template>
  <div>
    <h1 class="center">Welcome.</h1>
      <v-row>
          <v-col xs9>
              <v-text-field
                      name="repo-name"
                      label="Repo Name"
              ></v-text-field>
          </v-col>
          <v-col xs3>
              <v-btn light flat>Add Repo</v-btn>
          </v-col>
      </v-row>
      <h3 class="center"> Repos</h3>
      <RepoCard></RepoCard>
  </div>
</template>

<script>
  import RepoCard from './LandingPageView/RepoCard.vue';
  export default {
    components: {
      RepoCard,
    },
    name: 'landing-page',
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
</style>
