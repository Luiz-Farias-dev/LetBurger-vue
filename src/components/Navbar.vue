<template lang="">
  <nav>
    <router-link to="/" id="logo-url">
      <img id="logo" :src="logo" :alt="alt" />
    </router-link>
    <h1>Let Burguer</h1>
    <router-link to="/">Home</router-link>
    <router-link to="/pedidos">Pedidos</router-link>
  </nav>
</template>
<script>
export default {
  name: 'Navbar',
  props: ["logo", "alt"]
}
</script>
<style scoped>
  h1 {
    position: absolute;
    left: 100px;
    color: #FCBA03;
  }
  nav {
    background-color: #222;
    border-bottom: 4px solid #111;
    padding: 15px 50px;
    display: flex;
    justify-content: flex-end;
    align-items: center;
    position: relative;
    top: 0px;
    left: 0;
    height: 150px;
  }
  nav a {
    color: #FCBA03;
    text-decoration: none;
    margin: 12px;
    transition: .5s;
  }
  nav a:hover {
    color: #fff;
  } 
  #logo-url {
    position: absolute;
    left: 10px;
    top: auto;
    margin: auto;
    margin-left: 0;
  }
  #logo {
    width: 70px;
    height: 70px;
  }
</style>