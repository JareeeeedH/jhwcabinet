<template>
  <div class="">

    <body class="">

      <!-- <nav class="navbar navbar-expand-md navbar-light bg-transpatent">
        <div class="container">

          <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent">
            <span class="navbar-toggler-icon"></span>
          </button>

          <a class="navbar-brand d-flex align-items-center" href="#">
            <img src="img/logo_1.jpg" height="50" class="d-inline-block align-top" alt="logo">
            <span class="h3 px-2 mb-0 text-barMain font_2">Jared's Whiskey Cabinet</span>
          </a>
          <div class="dropdown order-md-1">
            <button style="cursor:pointer" class="btn btn-cart text-barMain type=" button" id="dropdownMenuButton"
              data-toggle="dropdown">
              <i class="fas fa-wine-bottle fa-2x abs"></i>
              <span class="badge badge-danger">2</span>
            </button>
            <div class="dropdown-menu dropdown-menu-right" style="min-width:360px" aria-labelledby="dropdownMenuButton">
              <table class="table">
                <tbody>
                  <tr>
                    <th scope="row"><i class="fas fa-trash-alt"></i></th>
                    <th>1</th>
                    <td>Ardbeg_10</td>
                    <td>6瓶</td>
                    <td class="text-right">6,000</td>
                  </tr>
                  <tr>
                    <th scope="row"><i class="fas fa-trash-alt"></i></th>
                    <th>2</th>
                    <td>A'bunadh</td>
                    <td>2瓶</td>
                    <td class="text-right">3,200</td>
                  </tr>
                </tbody>
              </table>
              <a class="btn btn-primary btn-block" href="cart.html">結帳</a>
            </div>
          </div>

          <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav ml-auto">
              <li class="nav-item active">
                <a class="nav-link nav_text" href="index.html">首頁 <span class="sr-only">(current)</span></a>
              </li>
              <li class="nav-item dropdown">
                <a class="nav-link dropdown-toggle nav_text" href="#" id="navbarDropdown" role="button"
                  data-toggle="dropdown" aria-haspopup="true">
                  服務
                </a>
                <div class="dropdown-menu" aria-labelledby="navbarDropdown">
                  <a class="dropdown-item" href="products_whiskey.html">Whiskey</a>
                  <a class="dropdown-item" href="#">Travel</a>
                  <div class="dropdown-divider"></div>
                  <a class="dropdown-item" href="#">Party</a>
                </div>
              </li>
              <li class="nav-item">
                <a class="nav-link nav_text" href="login.html">登入</a>
              </li>
            </ul>
          </div>


        </div>
      </nav> -->

      <div class="header jumbo-bg bg-cover d-flex mb-3">

        <div class="container d-flex justify-content-center align-items-center">

          <div class="row">

            <div class="col-12 d-flex align-items-center px-0 py-5">
              <div class="d-flex w-100 justify-content-between line">
                <div style="background-color: white;" class="steps_2 d-flex align-items-center justify-content-center">
                  <i class="fa fa-2x far fa-check-circle"></i></div>
                <div style="background-color: white;" class="steps_2 d-flex align-items-center justify-content-center">
                  <i class="fa fa-2x far fa-check-circle"></i></div>
                <div style="background-color: white;" class="steps_2 d-flex align-items-center justify-content-center">
                  <i class="fa fa-2x far fa-check-circle"></i></div>
              </div>
            </div>

            <div class="col-12">
              <h1 class="text-center text-white font-weight-bold">付款成功</h1>
            </div>

            <div class="col-12 text-center p-3 w-100" style='background-color: rgba(245, 234, 37, 0.7)'>
              <router-link  to="/index" class='h2 text-white'>
                繼續逛逛
              </router-link>
            </div>

          </div>


        </div>

      </div>

    </body>
  </div>
</template>

<script>


  export default {
    components: {
    },
    data() {
      return {
      }
    },

    methods: {

    },

  }

</script>


<style scoped>
.bg-cover{
    background-size: cover;
    background-position: center center
}

.jumbo-bg{
    background-image: url('../../assets/image/success.jpg');
    height: 496px;
}

.bg-lighter{
    background-color: rgb(255, 255, 255, 0.3)
}


.line::after{
    content:"";
    position: absolute;
    left:0;
    right:0;
    height: 1px;
    top: 50%;
    border: 1px solid white;
}

/* 0:還沒完成、 1當前步驟、 2完成 */
.steps_1{
    width:20px;
    height:20px;
    border: 1px solid white;
    border-radius: 20px;
    background-color: #0f3057;
    z-index:1;
    
}

.steps_1::after{
    content:"";
    position: absolute;
    width: 14px;
    height: 14px;
    background-color: white;
    border-radius: 20px;
}

.steps_0{
    width:20px;
    height:20px;
    border: 1px solid white;
    border-radius: 20px;
    background-color: #0f3057;
    z-index:1;
}

.steps_2{
    width:22px;
    height:22px;
    border: 1px solid white;
    border-radius: 20px;
    background-color: #0f3057;
    z-index:1;
    /* background-image: url('../img/done.svg'); */
}

</style>