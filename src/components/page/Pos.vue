<template>
  <div class="pos">
    <el-row>
      <el-col :span="7" class="pos-order" id="order-list">
            <el-tabs>
              <el-tab-pane label="点餐">
                <el-table
                  :data="tableData"
                  border
                  style="width: 100%">
                  <el-table-column prop="goodsName" label="商品"  width="110"></el-table-column>
                  <el-table-column prop="count" label="量" width="80"></el-table-column>
                  <el-table-column prop="price" label="金额" width="100"></el-table-column>
                  <el-table-column
                    fixed="right"
                    label="操作"
                    width="120">
                    <template slot-scope="scope">
                      <el-button @click="handleAdd(scope.row)" type="text" size="small">增加</el-button>
                      <el-button @click="handleDelete(scope.row)" type="text" size="small">删除</el-button>
                    </template>
                  </el-table-column>
                </el-table>
                <div class="div-btn">
                  <el-button type="warning">挂单</el-button>
                  <el-button type="danger">删除</el-button>
                  <el-button type="success">结账</el-button>
                </div>
              </el-tab-pane>
              <el-tab-pane label="挂单">
                挂单
              </el-tab-pane>
              <el-tab-pane label="外卖">
                外卖
              </el-tab-pane>
            </el-tabs>
      </el-col>
      <el-col :span="17" >
            <div class="often-goods">
              <div class="title">常用商品</div>
              <div class="often-goods-list">
                <ul>
                  <li v-for="item in oftenGoods">
                      <span>{{item.goodsName}}</span>
                      <span class="o-price">{{item.price}}</span>
                  </li>
                </ul>
              </div>
            </div>
        <div class="goods-type">

          <el-tabs>
            <el-tab-pane label="汉堡">
              <ul class='cookList'>
                <li v-for="goods in type0Goods">
                  <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                  <span class="foodName">{{goods.goodsName}}</span>
                  <span class="foodPrice">￥{{goods.price}}元</span>
                </li>
              </ul>
            </el-tab-pane>
            <el-tab-pane label="小食">
              <ul class='cookList'>
                <li v-for="goods in type1Goods">
                  <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                  <span class="foodName">{{goods.goodsName}}</span>
                  <span class="foodPrice">￥{{goods.price}}元</span>
                </li>
              </ul>
            </el-tab-pane>
            <el-tab-pane label="饮料">
              <ul class='cookList'>
                <li v-for="goods in type2Goods">
                  <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                  <span class="foodName">{{goods.goodsName}}</span>
                  <span class="foodPrice">￥{{goods.price}}元</span>
                </li>
              </ul>
            </el-tab-pane>
            <el-tab-pane label="套餐">
              <ul class='cookList'>
                <li v-for="goods in type3Goods">
                  <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                  <span class="foodName">{{goods.goodsName}}</span>
                  <span class="foodPrice">￥{{goods.price}}元</span>
                </li>
              </ul>
            </el-tab-pane>

          </el-tabs>
        </div>
      </el-col>

    </el-row>

  </div>
</template>

<script>
  import {oftenGoods,tableData,type0Goods} from '../../../static/analogData'
  export default {
    name: 'pos',
    data() {
      return {
        tableData:tableData,
        oftenGoods:[],
        type0Goods:[],
        type1Goods:[],
        type2Goods:[],
        type3Goods:[],
      }
    },
    methods: {
      handleAdd(index, row) {
        console.log(index, row);
      },
      handleDelete(index, row) {
        console.log(index, row);
      }
    },
    created(){
      this.$ajax.get('http://jspang.com/DemoApi/oftenGoods.php')
        .then(response=>{
          console.log(response);
          this.oftenGoods=response.data;
        })
        .catch(error=>{
          console.log(error);
          alert('网络错误，不能访问');
        });
      this.$ajax.get('http://jspang.com/DemoApi/typeGoods.php')
        .then(response=>{
          console.log(response);
          //this.oftenGoods=response.data;
          this.type0Goods=response.data[0];
          this.type1Goods=response.data[1];
          this.type2Goods=response.data[2];
          this.type3Goods=response.data[3];

        })
        .catch(error=>{
          console.log(error);
          alert('网络错误，不能访问');
        })
    },
    mounted:function(){
      var orderHeight=document.body.clientHeight;
      document.getElementById("order-list").style.height=orderHeight+'px';
    },
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
