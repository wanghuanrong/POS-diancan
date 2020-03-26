<template>
<div>
<h1>店铺</h1>
<ul v-for="list in list" :key="list.id">
    <li>{{list.goodsName}}</li>
    <li>{{list.price}}</li>
    <li>{{list.goodsName}}</li>
</ul>
</div>
    
</template>

<script>
import axios from 'axios';
export default {
    data:function(){
        return {
            list:[{
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
          }],
            msg:'成功！'
        }
    },
    // created(){
    //     axios.get('http://127.0.0.1:5500/tame1.json').then(response=>{
    //         this.list=response.data;
    //     }).catch(error=>{
    //         console.log(error);
    //     })
    // }
}
</script>


<style>
li{
    list-style:none;
}
</style>


