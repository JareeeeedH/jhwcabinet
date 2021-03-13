<template>
  <div class="hello">

    <div class="sticky-top">
      <Index_Navbar></Index_Navbar>
    </div>
    
    <div class="party">

      <h1>Party Services</h1>

      <div class="h5">
        <p>我們會指派一位專業的調酒師與一位DJ至您舉辦派對的位置。</p>
        <p>包辦現場所有燈光設施與DJ喇叭系統。</p>
        <p>酒水提供: Whiskey 與啤酒暢飲，一系列知名舞曲音樂撥放。</p>
        <p class="h5">請來信或來電洽詢與報價。</p>
      </div>
    </div>

  </div>

</template>

<script>
  import Index_Navbar from '../Index_Navbar';

  export default {
    components: {
      Index_Navbar,
    }
  }
</script>


<style>
  .party {
    background-image: url('../../assets/image/service_dj_aly.jpg');
    height: 500px;
    background-position: center center;
    background-size: cover;
    color: white;
    padding: 20px;
    margin-bottom: 50px;
  }
</style>