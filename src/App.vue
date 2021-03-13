<template>
  <div id="app">


    <div class="sticky-top">
      <!-- <Index_Navbar :shoppingList='cartList'></Index_Navbar> -->
    </div>




    <!-- 兩個router_view 示範。 -->
    <!-- <router-view name="menu"></router-view>    -->
    <div class="content">
      <router-view></router-view>
    </div>



    <!-- 全域插入Footer -->
    <div class="FOOTER">
      <Index_Footer />
    </div>


  </div>
</template>


<script>
  import Index_Footer from './components/Index_Footer';
  import Index_Navbar from './components/Index_Navbar';

  export default {
    name: 'App',
    components: {
      Index_Footer,
      Index_Navbar,
    },
    data() {
      return {
        cartList: {
          carts: {}
        },

      }
    },
    // methods: {
    //   getCart() {
    //     const api = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/cart`;
    //     const vm = this;

    //     this.$http.get(api).then((response) => {
    //       vm.cartList = response.data.data;
    //       console.log('購物車清單', response.data.data);
    //     })
    //   },

    // },
    // created() {
    //   this.getCart();
    // }
  }
</script>

<style lang="scss">
  @import "./assets/all.scss";


  /* 控制內容與 footer固定下方 */
  .content {
    min-height: calc(100vh - 70px);
  }

  .FOOTER {
    height: 70px;
  }
</style>