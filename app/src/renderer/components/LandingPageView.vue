<template>
  <div>
    <h1 class="center">Welcome</h1>
      <RepoSelect></RepoSelect>
    <h3 class="center"> Repos</h3>
      <RepoCard></RepoCard>
  </div>
</template>

<script>
  import RepoCard from './LandingPageView/RepoCard.vue';
  import RepoSelect from './LandingPageView/RepoSelect.vue';
  export default {
    components: {
      RepoCard,
      RepoSelect,
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
