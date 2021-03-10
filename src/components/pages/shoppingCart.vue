<template>
  <div class="">

    <!-- 痾樂 -->
    <Alert />


    <!-- Alert提示欄位 -->
    <div class="container py-5 text-center">
      <div class="form-row">
        <div class="col-12 col-sm">
          <div class="alert alert-primary alert-rounded" role="alert">
            1.輸入訂單資料
          </div>
        </div>
        <div class="col-12 col-sm">
          <div class="alert alert-dark alert-rounded" role="alert">
            2.選擇付款
          </div>
        </div>
        <div class="col-12 col-sm">
          <div class="alert alert-dark alert-rounded" role="alert">
            3.訂單完成
          </div>
        </div>
      </div>
    </div>

    <!-- 購物車列表；收展 -->

    <div class="row no-gutters justify-content-center">
      <div class="col-md-10 h3 p-4 my-3 text-center bg-light"><strong>訂單內容</strong></div>
    </div>
    <div class="row justify-content-center">
      <div class="col-md-10">
        <div class="card">
          <div class="card-header">
            <button class="btn btn-link" type="button" data-toggle="collapse" data-target="#collapseExample">
              顯示/隱藏訂購細項
            </button>
          </div>
          <div class="collapse card card-body" id="collapseExample">
            <div class="row justify-content-center">
              <div class="table-responsive">
                <table class="table">
                  <thead>
                    <tr>
                      <th scope="col" width="120">#</th>
                      <th scope="col">品名</th>
                      <th scope="col" width="80">數量</th>
                      <th scope="col">單價</th>
                      <th scope="col">小計</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="(cartItem, index) in cartList.carts">
                      <th scope="row">

                        <span>
                          {{index+1}}.<button class="btn btn-outline-danger btn-sm"
                            @click="delCart(cartItem)">刪除</button>
                        </span>

                      </th>

                      <td>
                        <span class="text-barMain font-weight-bold h5">{{cartItem.product.title}}</span>
                        <br>
                        <span class="text-success" v-if="cartItem.coupon">已套用優惠券</span>
                      </td>
                      <td>{{cartItem.qty}}</td>
                      <td>{{cartItem.product.price | currency}}</td>
                      <td>{{cartItem.total | currency}}</td>
                    </tr>
                    <tr>
                      <th scope="row"></th>
                      <td></td>
                      <td></td>
                      <td>總計:</td>
                      <td>{{cartList.total | currency}}</td>
                    </tr>
                    <tr v-if="cartList.final_total != cartList.total">
                      <th scope="row"></th>
                      <td></td>
                      <td></td>
                      <td class="text-success">折扣價:</td>
                      <td class="text-success">{{cartList.final_total | currency}}</td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </div>
          </div>
        </div>

        <!-- 折扣碼 -->
        <div class="row justify-content-center my-3">
          <div class="col-md-12">
            <span class="p-3 font-weight-bold">套用優惠碼:</span>
            <div class="p-3 font-weight-bold">店長當月壽星，約大家喝起來；輸入折扣碼享5%折扣: <span class="text-barMain font-weight-bold h3">drinkingUp</span></div>
            <div class="input-group mb-3">
              <input type="text" class="form-control" v-model="discountCode" placeholder="CuponCode">
              <div class="input-group-append">
                <button class="btn btn-outline-secondary" type="button" @click="getDiscount">套用優惠碼</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- 訂購表單 -->
    <div class="row no-gutters justify-content-center">
      <div class="col-md-10 h3 p-4 my-3 text-center bg-light"><strong>訂購人資料</strong></div>
    </div>

    <div class="my-5 row justify-content-center">

      <form class="col-md-10" @submit.prevent="creatOrder">
        <div class="form-group">
          <label for="useremail">Email</label>
          <input type="email" class="form-control" name="email" id="useremail" v-model="form.user.email"
            placeholder="請輸入 Email" required>
          <span class="text-danger">Email Address Please</span>
        </div>

        <div class="form-group">
          <label for="username">收件人姓名</label>
          <input type="text" class="form-control" name="name" id="username" v-model="form.user.name" placeholder="輸入姓名"
            required>
          <span class="text-danger">Do you know your name?</span>
        </div>

        <div class="form-group">
          <label for="usertel">收件人電話</label>
          <input type="tel" class="form-control" id="usertel" v-model="form.user.tel" placeholder="請輸入電話" required>
        </div>

        <div class="form-group">
          <label for="useraddress">收件人地址</label>
          <input type="text" class="form-control" name="address" id="useraddress" v-model="form.user.address"
            placeholder="請輸入地址" required>
          <span class="text-danger">地址欄位不得留空</span>
        </div>

        <div class="form-group">
          <label for="comment">留言</label>
          <textarea name="" id="comment" class="form-control" cols="30" rows="10" v-model="form.message"></textarea>
        </div>
        <div class="text-right">
          <button class="btn btn-danger">送出訂單</button>
        </div>
      </form>
    </div>

    <Index_Footer />

  </div>
</template>

<script>
  import Index_Navbar from '../Index_Navbar';
  import Index_Footer from '../Index_Footer';
  import Alert from '../AlertMessage'; //痾樂


  export default {
    name: 'shoppingCart',
    components: {
      Index_Navbar,
      Index_Footer,
      Alert,
    },

    data() {
      return {

        cartList: {
          carts:{}
        },

        discountCode: '', //優惠碼的資料、綁定欄位

        form: { //送出訂單的表單資料
          user: {
            name: 'Joy',
            email: 'oioi@gmail.com',
            tel: '0988-989-222',
            address: 'Kaohsiung'
          },
          message: 'Hello Vue'
        },
      }
    },

    methods: {
      // 取得購物車列表
      getCart() {
        const api = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/cart`;
        const vm = this;

        this.$http.get(api).then((response) => {
          vm.cartList = response.data.data;
          console.log('購物車清單', response.data.data);
        })
      },
      //套用優碼
      getDiscount() {
        const api = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/coupon`;
        const vm = this;

        const coupon = { code: vm.discountCode };

        this.$http.post(api, { data: coupon }).then((response) => {

          console.log(response.data)

          if (response.data.success) {
            this.$bus.$emit('message:push', '已套用優惠碼', 'success')
            vm.getCart();
          }
        })
      },
      delCart(cartItem) {
        const api = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/cart/${cartItem.id}`;
        const vm = this;

        this.$http.delete(api).then((response) => {

          if (response.data.success) {
            this.getCart();
            this.$bus.$emit('message:push', '已刪除', 'danger')
          }
        })
      },

      // 建立訂單
      creatOrder() {
        const api = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/order`;
        const vm = this;

        this.$http.post(api, { data: vm.form }).then((response) => {

          console.log('建立訂單', response.data)

          if (response.data.success) {
            this.$bus.$emit('message:push', '已建立訂單', 'success');
            vm.$router.push(`/customerOrder/${response.data.orderId}`);
          }

        })
      },


    },

    created() {
      this.getCart()
    },

  }

</script>


<style>

</style>