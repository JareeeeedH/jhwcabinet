<template>
  <div>

    <section class="bg-barMain">
      <div class="container">

        <nav class="navbar navbar-expand-md navbar-info">

          <!-- Logo -->
          <router-link class="navbar-brand shadow-none bg-transparent mr-auto" to="/home">
            <span class="h3 px-2 mb-0 text-white font_2">傑瑞酒業</span>
          </router-link>

          <!-- 購物車icon& dropDown-->
          <div class="dropdown order-md-1 mx-3">

            <button style="cursor:pointer" class="btn btn-cart text-white dropdown-toggle" type="button"
              id="dropdownMenuButton" data-toggle="dropdown">
              <i class="fas fa-wine-bottle fa-2x abs"></i>
              <span class="badge badge-danger">{{shoppingList.carts.length}}</span>
            </button>

            <div class="dropdown-menu dropdown-menu-right dropdown-md">
              <table class="table">
                <thead>
                  <tr>
                    <th scope="row"><i class="fas fa-trash-alt"></i></th>
                    <th>#</th>
                    <th>品名</th>
                    <th>數量</th>
                    <th>小計</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="(item,index) in shoppingList.carts">
                    <td scope="row">
                      <i class="fas fa-trash-alt"></i>
                    </td>

                    <td>{{index+1}}</td>
                    <td class="font-weight-bold">{{item.product.title}}</td>
                    <td>{{item.qty}}/{{item.product.unit}}</td>
                    <td class="text-right">{{item.final_total | currency}}</td>
                  </tr>
                </tbody>
                <tfoot>
                  <tr class="text-barMain h5 font-weight-bold">
                    <td scope="row" colspan="4" class="font-weight-bold h4 text-right">總計</td>
                    <td class="text-right">{{shoppingList.final_total | currency}}</td>
                  </tr>
                </tfoot>
              </table>
              <router-link class="btn btn-barMain btn-block" to="/shoppingCart">
                結帳去
              </router-link>
            </div>
          </div>

          <!-- 漢堡收合按鈕 -->
          <button class="navbar-dark border navbar-toggler" type="button" data-toggle="collapse"
            data-target="#navbarSupportedContent">
            <span class="navbar-toggler-icon"></span>
          </button>


          <!-- menu收合 -->
          <div class="collapse navbar-collapse" id="navbarSupportedContent">

            <!--預設Navbar與靠左顯示-->
            <div class="ml-auto d-none d-md-block">
              <ul class="navbar-nav ml-auto">
                <li class="nav-item active">
                  <router-link class="h5 mb-0 nav-link nav_text" to="/home">首頁 <span class="sr-only">(current)</span>
                  </router-link>
                </li>

                <li class="nav-item">
                  <router-link class="h5 mb-0 nav-link nav_text" to="/whiskey">威士忌</router-link>
                </li>

                <li class="nav-item">
                  <router-link class="h5 mb-0 nav-link nav_text" to="/travel">旅遊</router-link>
                </li>

                <li class="nav-item">
                  <router-link class="h5 mb-0 nav-link nav_text" to="/party">派對</router-link>
                </li>

                <li class="nav-item">
                  <router-link class="h5 mb-0 nav-link nav_text" to="/admin/products">登入</router-link>
                </li>
              </ul>
            </div>

            <!-- 小螢幕；收合內容 -->
            <div class="ml-auto d-md-none">
              <ul class="navbar-nav ml-auto d-flex flex-column align-items-center">
                <li class="nav-item active">

                  <router-link class="nav-link nav_text border-bottom" to="/index">
                    首頁
                  </router-link>
                </li>

                <li class="nav-item">
                  <router-link class="nav-link nav_text" to="/whiskey">威士忌</router-link>
                </li>

                <li class="nav-item">
                  <router-link class="nav-link nav_text" to="/travel">旅遊</router-link>
                </li>

                <li class="nav-item">
                  <router-link class="nav-link nav_text" to="/party">派對</router-link>
                </li>

                <li class="nav-item">
                  <router-link class="nav-link nav_text" to="/admin/products">登入</router-link>
                </li>
              </ul>

            </div>

          </div>



        </nav>

      </div>
    </section>

  </div>
</template>


<script>

  export default {
    name: 'IndexNavbar',
    props: ["shoppingList"], // 使用props接收資料。


  }
</script>