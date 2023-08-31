<script>
  import AppHeader from './components/AppHeader.vue';


  export default{
    name : 'App',
    components:{
      AppHeader,
    }
  }
</script>

<template>
  <header>
    <AppHeader />
  </header>

  <main>
    <router-view>
    </router-view>
  </main>

</template>

<style lang="scss">
@use './styles/general.scss' as *;

main{
  max-width: 1200px;
  margin: 0 auto;
  padding-top: 2rem;
}

</style>