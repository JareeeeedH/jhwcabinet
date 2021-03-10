<template>
  <div id="app">

  <!-- 全域插入NavBar；待確認。 -->
  <!-- <Index_Navbar :shoppingList='cartList'></Index_Navbar> -->



<!-- 兩個router_view 示範。 -->
      <!-- <router-view name="menu"></router-view>    -->
      <router-view></router-view>


<!-- 全域插入Footer -->
  <Index_Footer/>

  </div>
</template>


<script>
import Index_Footer from './components/Index_Footer';

  export default {
    name: 'App',
    components: {
            Index_Footer,
        },
  }
</script>

<style lang="scss">

    @import "./assets/all.scss";  

</style>    