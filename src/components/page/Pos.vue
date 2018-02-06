<template>
  <div class="pos">
    <el-row>
      <el-col :span="7" class="pos-order">
          <div class="grid-content bg-purple" id="order-list">
            我是订单栏
          </div>
      </el-col>
      <el-col >
          <div class="grid-content bg-purple-light">
              我是产品栏
          </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
  export default {
    name: 'pos',
    mounted:function(){
      var orderHeight=document.body.clientHeight;
      document.getElementById("order-list").style.height=orderHeight+'px';
    },
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
