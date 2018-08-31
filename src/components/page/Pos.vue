<template>
    <div class="pos">
        <el-row>
            <el-col :span='8' class="pos-order" id="order-List">
                <el-tabs>
                    <el-tab-pane label="点餐">
                        <el-table :data="tableData" border style="width=100%">
                            <el-table-column prop="goodsName" label="商品名称"></el-table-column>
                            <el-table-column prop="count" label="数量" width="60"></el-table-column>
                            <el-table-column prop="price" label="金额" width="100"></el-table-column>
                            <el-table-column label="操作" width="120" fixed="right">
                                <template slot-scope='scope'>
                                    <el-button type="text" size="small" @click="delSingleGoods(scope.row)">删除</el-button>
                                    <el-button type="text" size="small" @click="addOrderList(scope.row)">新增</el-button>
                                </template>
                            </el-table-column>
                        </el-table>
                        <div class="totalDiv">
                          <small>数量：</small><strong>{{totalCount}}</strong> &nbsp;&nbsp;&nbsp;&nbsp; <small> 金额：</small><strong>{{totalMoney}} 元</strong>
                        </div>
                        <div class="order-btn">
                            <el-button type="warning">挂单</el-button>
                            <el-button type="danger" @click="delAllGoods">删除</el-button>
                            <el-button type="success" @click="checkOut">结账</el-button>
                        </div>
                    </el-tab-pane>
                    <el-tab-pane label="挂单"></el-tab-pane>
                    <el-tab-pane label="外卖"></el-tab-pane>
                </el-tabs>
            </el-col>
            <el-col :span='16'>
                <div class="often-goods">
                    <div class="title">常用商品</div>
                    <div class="often-goods-list">
                        <ul>
                            <li v-for="goods in oftenGoods" @click="addOrderList(goods)">
                                <span >{{goods.goodsName}}</span>
                                <span class="o-price">￥{{goods.price}}元</span>
                            </li>
                        </ul>
                    </div>
                </div>
                <div class="goods-type">
                    <el-tabs>
                        <el-tab-pane label="汉堡">
                            <div>
                                <ul class="cookList">
                                    <li v-for='good in type0Goods'>
                                        <span class="foodImg"><img :src="good.goodsImg" width="100%"></span>
                                        <span class="foodName">{{good.goodsName}}</span>
                                        <span class="foodPrice">￥{{good.price}}元</span>
                                    </li>

                                </ul>
                            </div>
                        </el-tab-pane>
                        <el-tab-pane label="小吃">
                            <div>
                                <ul class="cookList">
                                    <li v-for='good in type1Goods'>
                                        <span class="foodImg"><img :src="good.goodsImg" width="100%"></span>
                                        <span class="foodName">{{good.goodsName}}</span>
                                        <span class="foodPrice">￥{{good.price}}元</span>
                                    </li>

                                </ul>
                            </div>
                        </el-tab-pane>
                        <el-tab-pane label="饮料">
                            <div>
                                <ul class="cookList">
                                    <li v-for='good in type2Goods'>
                                        <span class="foodImg"><img :src="good.goodsImg" width="100%"></span>
                                        <span class="foodName">{{good.goodsName}}</span>
                                        <span class="foodPrice">￥{{good.price}}元</span>
                                    </li>

                                </ul>
                            </div>
                        </el-tab-pane>
                        <el-tab-pane label="热能">
                            <div>
                                <ul class="cookList">
                                    <li v-for='good in type3Goods'>
                                        <span class="foodImg"><img :src="good.goodsImg" width="100%"></span>
                                        <span class="foodName">{{good.goodsName}}</span>
                                        <span class="foodPrice">￥{{good.price}}元</span>
                                    </li>

                                </ul>
                            </div>
                        </el-tab-pane>
                        <el-tab-pane label="水果">
                            <div>
                                <ul class="cookList">
                                    <li v-for='good in type4Goods'>
                                        <span class="foodImg"><img :src="good.goodsImg" width="100%"></span>
                                        <span class="foodName">{{good.goodsName}}</span>
                                        <span class="foodPrice">￥{{good.price}}元</span>
                                    </li>

                                </ul>
                            </div>
                        </el-tab-pane>
                    </el-tabs>
                </div>
            </el-col>
        </el-row>
    </div>
</template>
<script>
import axios from 'axios';
export default {
  name: "Pos", 
  data() {
    return {
      tableData: [
        {
          goodsName: "可口可乐",
          price: 8,
          count: 1
        },
        {
          goodsName: "香辣鸡腿堡",
          price: 15,
          count: 1
        },
        {
          goodsName: "爱心薯条",
          price: 8,
          count: 1
        },
        {
          goodsName: "甜筒",
          price: 8,
          count: 1
        }
      ],
      oftenGoods: [
        {
          goodsId: 1,
          goodsName: "香辣鸡腿堡",
          price: 18
        },
        {
          goodsId: 2,
          goodsName: "田园鸡腿堡",
          price: 15
        },
        {
          goodsId: 3,
          goodsName: "和风汉堡",
          price: 15
        },
        {
          goodsId: 4,
          goodsName: "快乐全家桶",
          price: 80
        },
        {
          goodsId: 5,
          goodsName: "脆皮炸鸡腿",
          price: 10
        },
        {
          goodsId: 6,
          goodsName: "魔法鸡块",
          price: 20
        },
        {
          goodsId: 7,
          goodsName: "可乐大杯",
          price: 10
        },
        {
          goodsId: 8,
          goodsName: "雪顶咖啡",
          price: 18
        },
        {
          goodsId: 9,
          goodsName: "大块鸡米花",
          price: 15
        },
        {
          goodsId: 20,
          goodsName: "香脆鸡柳",
          price: 17
        }
      ],
      type0Goods: [
        {
          goodsId: 1,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
          goodsName: "香辣鸡腿堡",
          price: 18
        },
        {
          goodsId: 2,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
          goodsName: "田园鸡腿堡",
          price: 15
        },
        {
          goodsId: 3,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
          goodsName: "和风汉堡",
          price: 15
        },
        {
          goodsId: 4,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
          goodsName: "快乐全家桶",
          price: 80
        },
        {
          goodsId: 5,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
          goodsName: "脆皮炸鸡腿",
          price: 10
        },
        {
          goodsId: 6,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
          goodsName: "魔法鸡块",
          price: 20
        },
        {
          goodsId: 7,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
          goodsName: "可乐大杯",
          price: 10
        },
        {
          goodsId: 20,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
          goodsName: "香脆鸡柳",
          price: 17
        }
      ],
      type1Goods:[
        {
          goodsId: 3,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
          goodsName: "和风汉堡",
          price: 15
        },
        {
          goodsId: 4,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
          goodsName: "快乐全家桶",
          price: 80
        },
        {
          goodsId: 5,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
          goodsName: "脆皮炸鸡腿",
          price: 10
        }
      ],
      type2Goods:[
        {
          goodsId: 3,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
          goodsName: "和风汉堡",
          price: 15
        },
        {
          goodsId: 4,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
          goodsName: "快乐全家桶",
          price: 80
        },
        {
          goodsId: 5,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
          goodsName: "脆皮炸鸡腿",
          price: 10
        }
      ],
      type3Goods:[
        {
          goodsId: 3,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
          goodsName: "和风汉堡",
          price: 15
        },
        {
          goodsId: 4,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
          goodsName: "快乐全家桶",
          price: 80
        },
        {
          goodsId: 5,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
          goodsName: "脆皮炸鸡腿",
          price: 10
        }
      ],
      type4Goods:[
        {
          goodsId: 3,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
          goodsName: "和风汉堡",
          price: 15
        },
        {
          goodsId: 4,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
          goodsName: "快乐全家桶",
          price: 80
        },
        {
          goodsId: 5,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
          goodsName: "脆皮炸鸡腿",
          price: 10
        }
      ],
      totalMoney:[],
      totalCount:[]
    };
  },
  // created:function(){
      // axios.get('http://jspang.com/DemoApi/typeGoods.php')
      // .then(reponse=>{
      //     console.log(reponse);
      //     this.type0Goods = Response.data[0];
      //     this.type1Goods = Response.data[1];
      //     this.type2Goods = Response.data[2];
      //     this.type3Goods = Response.data[3];
      //     this.type4Goods = Response.data[4];
      // })
      // .catch(error=>{
      //     console.log(error);
      //     alert('网络异常，不能访问');
      // })
  // },
  mounted: function() {
    var orderHeight = document.body.clientHeight;
    console.log(orderHeight);
    document.getElementById("order-List").style.height = orderHeight;
  },
  methods:{
      addOrderList(goods){
        this.totalMoney=0;
        this.totalCount=0;
        //商品是否存在订单列表中
        let ishava =false;
        for(let i=0;i<this.tableData.length;i++){
            if(this.tableData[i].goodsId == goods.goodsId){
                ishava = true;
            }
        }
        //根据判断的值编写业务逻辑
        if(ishava){
            let arr = this.tableData.filter(o=>o.goodsId == goods.goodsId);
            arr[0].count++;
        }else{
            //不存在就推入数组
            let newGoods = {goodsId:goods.goodsId,goodsName:goods.goodsName,price:goods.price,count:1}
            this.tableData.push(newGoods);
        }

        this.getAllMoney();
       
      },
      //删除单个商品
      delSingleGoods(goods){
        this.tableData=this.tableData.filter(o=>o.goodsId != goods.goodsId);
        this.getAllMoney();
      },
      delAllGoods(){
        this.tableData=[];
        this.totalMoney=0;
        this.totalCount=0;
      },
      // 模拟结账
      checkOut(){
        if(this.totalCount !=0){
          this.tableData=[];
          this.totalMoney=0;
          this.totalCount=0;
          this.$message({
            message:"感谢你的喜欢！",
            type:'success'
          })
        }else{
          // this.$message({
            // message:"淡定，朕还没点餐呢！",
            // type:'warning'
          // })
          this.$message.error('淡定，朕还没点餐呢！')
        }
      },
      // 汇总数量和总金额
      getAllMoney(){
        this.totalCount=0;
        this.totalMoney=0;
        if(this.tableData){
          // 计算汇总价格和数量
          this.tableData.forEach((element)=>{
            this.totalCount+=element.count;
            this.totalMoney= this.totalMoney + (element.price*element.count);
          })
        }
      }
  }
};
</script>
<style scoped>
.pos-order {
  background-color: #32da32;
  border-right: 1px solid #3ba1a1;
}
.order-btn {
  margin-top: 10px;
  text-align: center;
}
.title {
  height: 20px;
  border-bottom: 1px solid #d3d3d3;
  background-color: #3ba1a1;
  padding: 10px;
  text-align: center;
}
.often-goods-list ul li {
  list-style: none;
  float: left;
  border: 1px solid #dd1b21;
  padding: 10px;
  margin: 10px;
  background-color: #d3d3d3;
}
o-price {
  color: #dd1b21;
}
.goods-type {
  clear: both;
}
.cookList li {
  list-style: none;
  width: 15%;
  border: 1px solid #e5e9f2;
  height: auto;
  overflow: hidden;
  background-color: #fff;
  padding: 2px;
  float: left;
  margin: 2px;
}
.cookList li span {
    display: block;
    float:right;  
}
foodImg{
    width:40%;
}
.foodName {
  font-size: 16px;
  padding-left: 10px;
  color: rgb(243, 132, 132);
}
.foodPrice {
  font-size: 16px;
  padding-left: 10px;
  padding-top: 10px;
}
.totalDiv{
  background-color: #fff;
  padding:10px;
  border-bottom:1px solid #e5e9f2;  
  height:auot;
  font-size:16px;
  text-align:right;
  overflow: hidden;
}
</style>