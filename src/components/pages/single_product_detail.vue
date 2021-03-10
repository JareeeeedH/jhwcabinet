<template>
  <div class="hello bg-light">


    <div class="container">


      <!-- 麵包屑-->
      <nav aria-label="breadcrumb">
        <ol class="breadcrumb bg-transparent pl-0">
          <li class="breadcrumb-item">
            <router-link to="/index">首頁</router-link>
          </li>
          <li class="breadcrumb-item">
            <router-link to="/whiskey">Whiskey</router-link>
          </li>
          <li class="breadcrumb-item active">Ardbeg10</li>
        </ol>
      </nav>

      <div class="row mb-5">
        <div class="col-md-4">
          <div class="sticky-top" style='top:20px'>
            <div>
              <h1 class="mb-3">Ardbeg 10</h1>
              <div class="d-flex justify-content-end align-items-end">
                <span><del>售價$1,250</del></span>
                <div class="h3 text-danger ml-auto mb-0">
                  <small>特價</small>
                  <strong>1,050</strong>
                </div>
              </div>
              <hr> 單位:
              <div class="btn-group btn-group-toggle btn-group-sm" data-toggle="buttons">
                <label class="btn btn-outline-secondary disabled">
                  <input type="radio" name="options" id="option1" autocomplete="off"> 杯
                </label>
                <label class="btn btn-outline-secondary">
                  <input type="radio" name="options" id="option2" autocomplete="off"> 瓶
                </label>
                <label class="btn btn-outline-secondary">
                  <input type="radio" name="options" id="option3" autocomplete="off"> 打
                </label>
              </div>

              <div class="input-group input-group-sm mt-3">
                <select class="form-control mr-2">
                  <option selected value="1">One</option>
                  <option value="2">Two</option>
                  <option value="3">Three</option>
                </select>
                <a href="#" class="btn btn-sm btn-primary">加入購物車</a>
              </div>
            </div>
          </div>
        </div>
        <div class="col-md-8">
          <div class="d-flex flex-column">
            <div class="h1">{{product.product.title}}</div>

            <p>
              {{product.product.content}}
            </p>

            <strong class="h3 text-center">
              {{product.product.description}}
            </strong>
            <div class="bg-cover" style="height: 550px" :style="{backgroundImage: `url(${product.product.imageUrl})`}">

            </div>

          </div>
        </div>
      </div>
    </div>



  </div>

</template>

<script>

  export default {
    components: {

    },

    data() {
      return {
        product: {}, //單一筆產品data
        nowID: '',
      }
    },

    methods: {
      // 取路由參數ID、串API、取單一產品內容
      getSingleDetail() {

        this.nowID = this.$route.params.productID;
        const api = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/product/${this.nowID}`;

        const vm = this;

        this.$http.get(api).then((response) => {

          console.log('單一產品細節:', response.data);

          if (response.data.success == true) {
            vm.product = response.data;
          }

        })
      },




      // 加入購物車
      addtoCart(id, qty = 1) {
        const api = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/cart`;
        const vm = this;
        this.status.loadingItem = `${id}`; //讀取出現

        // 加入購物車所需丟入的資料結構。
        const addingItem = {
          product_id: id,
          qty: qty,
        };

        this.$http.post(api, { data: addingItem }).then((response) => {
          console.log(response.data);

          vm.status.loadingItem = '' //讀取消失

          $('#productModal').modal('hide')
          this.$bus.$emit('message:push', '已加入購物車', 'success')

        })

      },

    },

    created() {
      this.getSingleDetail();
    }

  }

</script>

<style scoped>

</style>