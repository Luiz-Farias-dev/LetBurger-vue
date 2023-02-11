<template>
  <main>
    <Navbar :logo="logo_src" :alt="alt_src"/>
    <router-view></router-view>
    <FooterComponent />
  </main>
</template>

<script>
  import Navbar from './components/Navbar.vue';
  import FooterComponent from './components/FooterComponent.vue';

  export default {
    name: 'App',
    components: {
      Navbar,
      FooterComponent,
    },
    data() {
      return{
        logo_src: '/imgs/logo.png',
        alt_src: 'Logo do site'
      }
      
    }
  }
</script>


<style>
  * {
    padding: 0;
    margin: 0;
    font-family: Helvetica, sans-serif;
    box-sizing: border-box;
  }
  .main-container {
    margin: 50px;
    min-height: 250px;
  }
  .main-container h1 {
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
  }
</style>
