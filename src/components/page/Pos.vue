<template>
  <div id="pos">
    <div>
      <el-row>
        <!-- 左边结账栏 -->
        <el-col :span='7' id="order-list" >
          <el-tabs>
            <el-tab-pane label="点餐">
              <el-table border style="width:100%" :data="tableData">
                <el-table-column prop="goodsName" label="商品" class="etc" ></el-table-column>
                <el-table-column prop="count" label="数量" width="50"></el-table-column>
                <el-table-column prop="price" label="金额" width="70"></el-table-column>
                <el-table-column  label="操作" width="100" fixed="right"> 
                  <template scope="scope">
                    <el-button type="text" size="small" @click="delSingleGoods(scope.row)">删除</el-button>
                    <el-button type="text" size="small" @click="addOrderList(scope.row)">增加</el-button>
                  </template>
                </el-table-column>
              </el-table>
              <div class="totalDiv">
                                <small>数量：</small>
                                <strong>{{totalCount}}</strong> &nbsp;&nbsp;&nbsp;&nbsp;
                                <small>总计：</small>
                                <strong>{{totalMoney}}</strong> 元
                            </div>

              <div id="div-btn">
                <el-button type="warning">挂单</el-button>
                <el-button type="danger" @click="delAllGoods">删除</el-button>
                <el-button type="success" @click="checkout">结账</el-button>
              </div>
            </el-tab-pane>


            <el-tab-pane label="外卖">外卖</el-tab-pane>
            <el-tab-pane label="挂单">挂单</el-tab-pane>
          </el-tabs>
        </el-col>


         <!-- 右边产品栏 , 上部分-->
        <el-col :span='17'>
          <div class="ofter-goods">
            <div class="title">常用商品</div>
            <div class="ofter-goods-list">
              <ul>
                <li v-for="goods in oftenGoods" :key="goods.id" @click="addOrderList(goods)">
                  <span>{{goods.goodsName}}</span>
                  <span class="o-price">￥{{goods.price}}元</span>
                </li>
              </ul>
            </div>

            <!-- 右边产品栏 ， 下部分 -->
            <div class="goods-type">
               <el-tabs>
                <el-tab-pane label="汉堡">
                    <ul class='cookList'>
                        <li v-for="goods in type0Goods" :key="goods.id" @click="addOrderList(goods)">
                            <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                            <span class="foodName">{{goods.goodsName}}</span>
                            <span class="foodPrice">￥{{goods.price}}元</span>
                        </li>
                    </ul>
                </el-tab-pane>
                <el-tab-pane label="小食">
                   <ul class='cookList'>
                        <li v-for="goods in type1Goods" :key="goods.id" @click="addOrderList(goods)">
                            <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                            <span class="foodName">{{goods.goodsName}}</span>
                            <span class="foodPrice">￥{{goods.price}}元</span>
                        </li>
                    </ul>
                </el-tab-pane>
                <el-tab-pane label="饮料">
                    <ul class='cookList'>
                        <li v-for="goods in type2Goods" :key="goods.id" @click="addOrderList(goods)">
                            <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                            <span class="foodName">{{goods.goodsName}}</span>
                            <span class="foodPrice">￥{{goods.price}}元</span>
                        </li>
                    </ul>
                </el-tab-pane>
                <el-tab-pane label="套餐">
                   <ul class='cookList'>
                        <li v-for="goods in type3Goods" :key="goods.id" @click="addOrderList(goods)">
                            <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                            <span class="foodName">{{goods.goodsName}}</span>
                            <span class="foodPrice">￥{{goods.price}}元</span>
                        </li>
                    </ul>
                </el-tab-pane>
    
              </el-tabs>
            </div>
            
          </div>
        </el-col>

        

      </el-row>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'pos',
  data(){
    return{
      tableData: [],
        oftenGoods:[{
              goodsId:1,
              goodsName:'香辣鸡腿堡',
              price:18
          }, {
              goodsId:2,
              goodsName:'田园鸡腿堡',
              price:15
          }, {
              goodsId:3,
              goodsName:'和风汉堡',
              price:15
          }, {
              goodsId:4,
              goodsName:'快乐全家桶',
              price:80
          }, {
              goodsId:5,
              goodsName:'脆皮炸鸡腿',
              price:10
          }, {
              goodsId:6,
              goodsName:'魔法鸡块',
              price:20
          }, {
              goodsId:7,
              goodsName:'可乐大杯',
              price:10
          }, {
              goodsId:8,
              goodsName:'雪顶咖啡',
              price:18
          }, {
              goodsId:9,
              goodsName:'大块鸡米花',
              price:15
          }, {
              goodsId:20,
              goodsName:'香脆鸡柳',
              price:17
          }],
        type0Goods:[{
              goodsId:1,
              goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
              goodsName:'香辣鸡腿堡',
              price:18
          }, {
              goodsId:2,
              goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
              goodsName:'田园鸡腿堡',
              price:15
          }, {
              goodsId:3,
              goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
              goodsName:'和风汉堡',
              price:15
          }, {
              goodsId:4,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
              goodsName:'快乐全家桶',
              price:80
          }, {
              goodsId:5,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
              goodsName:'脆皮炸鸡腿',
              price:10
          }, {
              goodsId:6,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
              goodsName:'魔法鸡块',
              price:20
          }, {
              goodsId:7,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
              goodsName:'可乐大杯',
              price:10
          }, {
              goodsId:8,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
              goodsName:'雪顶咖啡',
              price:18
          }, {
              goodsId:9,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
              goodsName:'大块鸡米花',
              price:15
          }, {
              goodsId:20,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
              goodsName:'香脆鸡柳',
              price:17
          }],
        type1Goods:[{
              goodsId:1,
              goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
              goodsName:'麻辣香锅',
              price:18
          }, {
              goodsId:2,
              goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
              goodsName:'火腿炒蛋',
              price:15
          }, {
              goodsId:3,
              goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
              goodsName:'辣椒炒肉',
              price:15
          }, {
              goodsId:4,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
              goodsName:'鸭腿饭',
              price:80
          }, {
              goodsId:5,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
              goodsName:'酸辣土豆丝',
              price:10
          }, {
              goodsId:6,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
              goodsName:'蛋炒饭',
              price:20
          }, {
              goodsId:7,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
              goodsName:'大杯雪碧',
              price:10
          }, {
              goodsId:8,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
              goodsName:'营养快线',
              price:18
          }, {
              goodsId:9,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
              goodsName:'爆米花',
              price:15
          }, {
              goodsId:20,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
              goodsName:'炸鸡翅',
              price:17
          }],
        type2Goods:[{
              goodsId:1,
              goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
              goodsName:'啤酒鸭',
              price:18
          }, {
              goodsId:2,
              goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
              goodsName:'辣子鸡丁',
              price:15
          }, {
              goodsId:3,
              goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
              goodsName:'豆角炒肉',
              price:15
          }, {
              goodsId:4,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
              goodsName:'红烧鱼块',
              price:80
          }, {
              goodsId:5,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
              goodsName:'烤鸡腿',
              price:10
          }, {
              goodsId:6,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
              goodsName:'烤鸭腿',
              price:20
          }, {
              goodsId:7,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
              goodsName:'冰红茶',
              price:10
          }, {
              goodsId:8,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
              goodsName:'抄猪皮',
              price:18
          }, {
              goodsId:9,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
              goodsName:'麻辣小龙虾',
              price:15
          }, {
              goodsId:20,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
              goodsName:'红烧鸡屁股',
              price:17
          }],
        type3Goods:[{
              goodsId:1,
              goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
              goodsName:'鸭血粉丝',
              price:18
          }, {
              goodsId:2,
              goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
              goodsName:'牛肉粉丝',
              price:15
          }, {
              goodsId:3,
              goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
              goodsName:'小炒牛肉',
              price:15
          }, {
              goodsId:4,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
              goodsName:'快乐全家桶',
              price:80
          }, {
              goodsId:5,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
              goodsName:'脆皮炸鸡腿',
              price:10
          }, {
              goodsId:6,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
              goodsName:'魔法鸡块',
              price:20
          }, {
              goodsId:7,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
              goodsName:'可乐大杯',
              price:10
          }, {
              goodsId:8,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
              goodsName:'雪顶咖啡',
              price:18
          }, {
              goodsId:9,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
              goodsName:'大块鸡米花',
              price:15
          }, {
              goodsId:20,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
              goodsName:'香脆鸡柳',
              price:17
          }],
        totalCount:0,
        totalMoney:0

    }
  },created(){
    axios.get('https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/oftenGoods')
    .then(response=>{
      this.oftenGoods=response.data;
    })
    .catch(error=>{
      alert('网络错误，不能访问')
    });


    axios.get('https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/typeGoods')
    .then(response=>{
      this.type0Goods=response.data[0];
      this.type1Goods=response.data[1];
      this.type2Goods=response.data[2];
      this.type3Goods=response.data[3];
    })
    .catch(error=>{
      alert('网络错误，不能访问')
    })
  },
  mounted(){
    var orderHeight=document.body.clientHeight;
    document.getElementById('order-list').style.height=orderHeight+'px';
  },
  methods:{
      //添加订单列表的方法
      addOrderList(goods){
            // this.totalCount=0; //汇总数量清0
            // this.totalMoney=0;
            let isHave=false;
            //判断是否这个商品已经存在于订单列表
            for (let i=0; i<this.tableData.length;i++){
                console.log(this.tableData[i].goodsId);
                if(this.tableData[i].goodsId==goods.goodsId){
                    isHave=true; //存在
                }
            }
            //根据isHave的值判断订单列表中是否已经有此商品
            if(isHave){
                //存在就进行数量添加
                 let arr = this.tableData.filter(o =>o.goodsId == goods.goodsId);
                 arr[0].count++;
                 //console.log(arr);
            }else{
                //不存在就推入数组
                let newGoods={goodsId:goods.goodsId,goodsName:goods.goodsName,price:goods.price,count:1};
                 this.tableData.push(newGoods);
 
            }
 
            //进行数量和价格的汇总计算
            // this.tableData.forEach((element) => {
            //     this.totalCount+=element.count;
            //     this.totalMoney=this.totalMoney+(element.price*element.count);   
            // });

            this.getAllMoney();
           
      },
      // 点击删除商品
      delSingleGoods(goods){
        this.tableData=this.tableData.filter(o=>o.goodsId != goods.goodsId);
        this.getAllMoney();
      },
      // 汇总数量和金额
      getAllMoney(){
        this.totalCount=0; //汇总数量清0
        this.totalMoney=0;

        this.tableData.forEach((element) => {
                this.totalCount+=element.count;
                this.totalMoney=this.totalMoney+(element.price*element.count);   
            });
      },
      // 删除所有商品
      delAllGoods(){
        this.tableData=[];
        this.totalCount=0;
        this.totalMoney=0;
      },
      checkout() {
          if (this.totalCount!=0) {
              this.tableData = [];
              this.totalCount = 0;
              this.totalMoney = 0;
              this.$message({
                  message: '结账成功，感谢你又为店里出了一份力!',
                  type: 'success'
              });
      
          }else{
              this.$message.error('不能空结。老板了解你急切的心情！');
          }
      
      }
  }
  }

</script>

<style scoped>
/* .order-list{
  background-color: red;
  height: 100%;
} */
*{
  text-align: center;
}

#order-list{
  background-color: white;
}

#div-btn{
  margin: 10px;
}

.title{
  height: 20px;
  border-bottom: 1px solid #D3DCE6;
  background-color: #F9FAFC;
  padding: 10px;
  text-align: left;
}

.ofter-goods-list ul li{
  list-style:none;
  float: left;
  border: 1px solid #E5E9F2;
  padding: 10px;
  margin: 5px;
  background-color: #fff;
  cursor: pointer;
}

.o-price{
  color: #58B7FF; 
}

.cookList li{
       list-style: none;
       width:23%;
       border:1px solid #E5E9F2;
       height: auot;
       overflow: hidden;
       background-color:#fff;
       padding: 2px;
       float:left;
       margin: 2px;
       cursor: pointer;
 
   }
   .cookList li span{
       
        display: block;
        float:left;
   }
   .foodImg{
       width: 40%;
   }
   .foodName{
       font-size: 18px;
       padding-left: 10px;
       color:brown;
 
   }
   .foodPrice{
       font-size: 16px;
       padding-left: 10px;
       padding-top:10px;
   }

   .goods-type{
     clear: both;
   }

  .etc{
    margin-left: 15px;
  }
</style>
