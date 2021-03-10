<template>
  <div class="">

    <!-- 讀取效果元件 -->
    <loading :active.sync="isLoading">
    </loading>


    <!-- 產品頁面的NavBar -->
    <!-- <Index_Navbar :shoppingList='cartList'></Index_Navbar> -->

    <!-- 一個卡片、產品欄位；使用v-for渲染所有產品 -->
    <div class="row mt-4">
      <div class="col-md-4 mb-4" v-for="item in products" :key="item.id">
        <div class="card border shadow-sm">
          <div style="height: 280px; background-size: cover; background-position: center center"
            :style="{backgroundImage: `url(${item.imageUrl})`}">
          </div>
          <div class="card-body">
            <span class="badge badge-secondary float-right ml-2">{{ item.category }}</span>
            <h5 class="card-title">
              <a href="#" class="text-barMain font-weight-bold">{{ item.title }}</a>
            </h5>
            <p class="card-text">{{ item.content }}</p>
            <div class="d-flex justify-content-between align-items-baseline">
              <div class="h5" v-if="!item.price">{{ item.origin_price | currency}} 元</div>
              <del class="h6" v-if="item.price">原價 {{ item.origin_price | currency}} 元</del>
              <div class="h5" v-if="item.price">現在只要 {{ item.price | currency}} 元</div>
            </div>
          </div>
          <div class="card-footer d-flex">
            <button type="button" class="btn btn-outline-secondary btn-sm" @click="getSingleProduct(item.id)">
              <i class="fas fa-spinner fa-spin" v-if="status.loadingItem==item.id"></i>
              查看更多
            </button>
            <button type="button" class="btn btn-outline-danger btn-sm ml-auto" @click="addtoCart(item.id)">
              <i class="fas fa-spinner fa-spin" v-if="status.loadingItem==item.id"></i>
              加到購物車
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- "查看更多"的Modal -->
    <div class="modal fade" id="productModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel"
      aria-hidden="true">
      <div class="modal-dialog" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">{{ product.title }}</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <img :src="product.imageUrl" class="img-fluid" alt="productPhoto">
            <blockquote class="blockquote mt-3">
              <p class="mb-0">{{ product.content }}</p>
              <footer class="blockquote-footer text-right">{{ product.description }}</footer>
            </blockquote>
            <div class="d-flex justify-content-between align-items-baseline">
              <div class="h4" v-if="!product.price">{{ product.origin_price }} 元</div>
              <del class="h6" v-if="product.price">原價 {{ product.origin_price }} 元</del>
              <div class="h4" v-if="product.price">現在只要 {{ product.price }} 元</div>
            </div>
            <select name="qty" class="form-control mt-3" v-model="product.Qty">
              <option value="0" disabled selected>請選擇數量</option>
              <option :value="num" v-for="num in 6" :key='num'>選{{ num }} {{ product.unit}}</option>
            </select>
          </div>
          <div class="modal-footer">
            <div class="text-muted text-nowrap mr-3">
              小計 <strong>{{ product.Qty * product.price }}</strong> 元
            </div>
            <button type="button" class="btn btn-primary" @click="addtoCart(product.id, product.Qty)">
              <i class="fas fa-spinner fa-spin" v-if="status.loadingItem==product.id"></i>
              加到購物車
            </button>
          </div>
        </div>
      </div>>
    </div>


  </div>
</template>

<script>
  import Index_Navbar from '../Index_Navbar';


  export default {
    name: 'Whiskey',
    components: {
      Index_Navbar,
    },
    data() {
      return {
        products: {}, //所有產品data

        product: {}, //單一筆產品data

        isLoading: false, //全域loading控制

        status: {
          loadingItem: '', //讀取icon顯示/出現控制
        },

      }
    },

    methods: {
      //取得產品列表
      getProducts() {
        const api = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/products/all`;
        // const api = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/admin/products/all`;
        // const api = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/admin/products`;
        // const api = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/products?page=${page}`;
        const vm = this;

        vm.isLoading = true; //打開全域讀取

        this.$http.get(api).then((response) => {

          console.log('產品列表:', response.data);
          vm.isLoading = false; // 結束全域讀取
          vm.products = response.data.products;

        })
      },
      //取得單一筆產品
      getSingleProduct(id) {

        this.status.loadingItem = `${id}`; //讀取出現

        const api = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/product/${id}`;
        const vm = this;

        this.$http.get(api).then((response) => {
          console.log('單一筆產品', response.data);
          vm.product = response.data.product;

          vm.status.loadingItem = '' //讀取消失
          $('#productModal').modal('show');

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
      this.getProducts();

      // event bus的使用方法；、載入元件後；可將這段用於任何要顯示的地方。
      this.$bus.$emit('message:push', 'HelloWorld', 'info')
    },


  }

</script>


<style>
  @import "../../assets/helpers/service_whiskey_style.sass";
</style>