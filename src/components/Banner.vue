<template>
  <div id="main-banner">
    <h1>Make Your Burger</h1>
  </div>
</template>
<script>
export default {
  name: 'Banner',
}
</script>
<style scoped>
  #main-banner {
    background: url(/imgs/burger.jpg) no-repeat;
    background-size: auto;
    background-position: 0 -280px;
    height: 750px;
    display: flex;
    align-items: center;
    justify-content: flex-start;
  }
  #main-banner h1 {
    color: #fff;
    text-align: center;
    font-size: 60px;
    background-color: #222 ;
    padding: 20px 40px;
  }
</style>
 