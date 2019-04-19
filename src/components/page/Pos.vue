<template>
  <div class="pos">
  	<div>
  		<el-row>
  			<el-col :span='7' class="pos-order" id="order-list">
  				<el-tabs type="border-card">
			      <el-tab-pane label="点餐">
				       		<el-table :data="tableData" border style="width: 100%">
			  					<el-table-column prop="goodsName" label="商品">
			    				</el-table-column>
			    				<el-table-column prop="count" label="数量" width="50">
			    				</el-table-column>
			    				<el-table-column prop="price" label="金额" width="60">
			    				</el-table-column>
			    				<el-table-column prop="goodname" label="操作" width="100%" fixed="right">
		    					<template slot-scope="scope">
		            				<el-button type="text" size="small" @click="delSingleGoods(scope.row)">删除</el-button>
		            				<el-button type="text" size="small" @click="addOrderList(scope.row)">增加</el-button>
		        				</template>	
	    						</el-table-column>
	  				  		</el-table>
	  				  		<div>
	  				  			<span>数量：</span><span>{{totalCount}}</span>
	  				  			<span>总价：</span><span>{{totalMoney}}</span>
	  				  		</div>
			  				<div class="div-btn">
			  				  	<el-button type="warning" >挂单</el-button>
								<el-button type="danger" @click="delAllGoods()">删除</el-button>
								<el-button type="success" >结账</el-button>
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
  			<el-col :span='17'>
  				<div class="often-goods">
  					<div class="title">常用商品</div>
  					<div class="often-goods-list">
  						<ul>
  							<li v-for="goods in oftenGoods" @click="addOrderList(goods)">
  								<span>{{goods.goodsName}}</span>
  								<span class="0-price">￥{{goods.price}}</span>
  							</li>
  						</ul>
  					</div>
  				</div>
  				<div class="goods-type">
  					<el-tabs>
  						<el-tab-pane label="汉堡">
				            <ul class='cookList'>
							    <li v-for="goods in type0Goods" @click="addOrderList(goods)">
							        <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
							        <span class="foodName">{{goods.goodsName}}</span>
							        <span class="foodPrice">￥{{goods.price}}元</span>
							    </li>
							</ul>
				        </el-tab-pane>
				        <el-tab-pane label="小食">
				            <ul class='cookList'>
							    <li v-for="goods in type1Goods" @click="addOrderList(goods)">
							        <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
							        <span class="foodName">{{goods.goodsName}}</span>
							        <span class="foodPrice">￥{{goods.price}}元</span>
							    </li>
							</ul>
				        </el-tab-pane>
				        <el-tab-pane label="饮料">
				            <ul class='cookList'>
							    <li v-for="goods in type2Goods" @click="addOrderList(goods)">
							        <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
							        <span class="foodName">{{goods.goodsName}}</span>
							        <span class="foodPrice">￥{{goods.price}}元</span>
							    </li>
							</ul>
				        </el-tab-pane>
				        <el-tab-pane label="套餐">
				            <ul class='cookList'>
							    <li v-for="goods in type3Goods" @click="addOrderList(goods)">
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
  	<!-- hello my pos -->
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Pos',
  data(){
  	return {
  	    tableData:[],
        oftenGoods:[
          // {
          //     goodsId:1,
          //     goodsName:'香辣鸡腿堡',
          //     price:18
          // }, {
          //     goodsId:2,
          //     goodsName:'田园鸡腿堡',
          //     price:15
          // }, {
          //     goodsId:3,
          //     goodsName:'和风汉堡',
          //     price:15
          // }, {
          //     goodsId:4,
          //     goodsName:'快乐全家桶',
          //     price:80
          // }, {
          //     goodsId:5,
          //     goodsName:'脆皮炸鸡腿',
          //     price:10
          // }, {
          //     goodsId:6,
          //     goodsName:'魔法鸡块',
          //     price:20
          // }, {
          //     goodsId:7,
          //     goodsName:'可乐大杯',
          //     price:10
          // }, {
          //     goodsId:8,
          //     goodsName:'雪顶咖啡',
          //     price:18
          // }, {
          //     goodsId:9,
          //     goodsName:'大块鸡米花',
          //     price:15
          // }, {
          //     goodsId:20,
          //     goodsName:'香脆鸡柳',
          //     price:17
          // }
        ],
      	type0Goods:[
          // {
          //     goodsId:1,
          //     goodsImg:"https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1539021414790&di=edb1c382e3a8fcc16297f09aefd004b3&imgtype=0&src=http%3A%2F%2Ffile1.foodmate.net%2Ffile%2Fupload%2F201404%2F18%2F13-52-00-91-543665.jpg",
          //     goodsName:'香辣鸡腿堡',
          //     price:18
          // }, {
          //     goodsId:2,
          //     goodsImg:"https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1539021414790&di=edb1c382e3a8fcc16297f09aefd004b3&imgtype=0&src=http%3A%2F%2Ffile1.foodmate.net%2Ffile%2Fupload%2F201404%2F18%2F13-52-00-91-543665.jpg",
          //     goodsName:'田园鸡腿堡',
          //     price:15
          // }, {
          //     goodsId:3,
          //     goodsImg:"https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1539021414790&di=edb1c382e3a8fcc16297f09aefd004b3&imgtype=0&src=http%3A%2F%2Ffile1.foodmate.net%2Ffile%2Fupload%2F201404%2F18%2F13-52-00-91-543665.jpg",
          //     goodsName:'和风汉堡',
          //     price:15
          // }, {
          //     goodsId:4,
          //      goodsImg:"https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1539021414790&di=edb1c382e3a8fcc16297f09aefd004b3&imgtype=0&src=http%3A%2F%2Ffile1.foodmate.net%2Ffile%2Fupload%2F201404%2F18%2F13-52-00-91-543665.jpg",
          //     goodsName:'快乐全家桶',
          //     price:80
          // }, {
          //     goodsId:5,
          //      goodsImg:"https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1539021414790&di=edb1c382e3a8fcc16297f09aefd004b3&imgtype=0&src=http%3A%2F%2Ffile1.foodmate.net%2Ffile%2Fupload%2F201404%2F18%2F13-52-00-91-543665.jpg",
          //     goodsName:'脆皮炸鸡腿',
          //     price:10
          // }, {
          //     goodsId:6,
          //      goodsImg:"https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1539021414790&di=edb1c382e3a8fcc16297f09aefd004b3&imgtype=0&src=http%3A%2F%2Ffile1.foodmate.net%2Ffile%2Fupload%2F201404%2F18%2F13-52-00-91-543665.jpg",
          //     goodsName:'魔法鸡块',
          //     price:20
          // }, {
          //     goodsId:7,
          //      goodsImg:"https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1539021414790&di=edb1c382e3a8fcc16297f09aefd004b3&imgtype=0&src=http%3A%2F%2Ffile1.foodmate.net%2Ffile%2Fupload%2F201404%2F18%2F13-52-00-91-543665.jpg",
          //     goodsName:'可乐大杯',
          //     price:10
          // }, {
          //     goodsId:8,
          //      goodsImg:"https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1539021414790&di=edb1c382e3a8fcc16297f09aefd004b3&imgtype=0&src=http%3A%2F%2Ffile1.foodmate.net%2Ffile%2Fupload%2F201404%2F18%2F13-52-00-91-543665.jpg",
          //     goodsName:'雪顶咖啡',
          //     price:18
          // }, {
          //     goodsId:9,
          //      goodsImg:"https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1539021414790&di=edb1c382e3a8fcc16297f09aefd004b3&imgtype=0&src=http%3A%2F%2Ffile1.foodmate.net%2Ffile%2Fupload%2F201404%2F18%2F13-52-00-91-543665.jpg",
          //     goodsName:'大块鸡米花',
          //     price:15
          // }, {
          //     goodsId:20,
          //      goodsImg:"https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1539021414790&di=edb1c382e3a8fcc16297f09aefd004b3&imgtype=0&src=http%3A%2F%2Ffile1.foodmate.net%2Ffile%2Fupload%2F201404%2F18%2F13-52-00-91-543665.jpg",
          //     goodsName:'香脆鸡柳',
          //     price:17
          // }
      	],
      	type1Goods:[],
      	type2Goods:[],
      	type3Goods:[],
      	totalMoney:0,
      	totalCount:0
  	}
  },
  created(){
  	//读取商品列表
      axios.get('api/oftenGoods')
      .then(response=>{
      	console.log(response,'请求成功');
      	this.oftenGoods=response.data;
      })
      .catch(error=>{
      	console.log(error,'请求失败')
      })

      axios.get('api/typeGoods')
      .then(response=>{
      	this.type0Goods=response.data[0];
      	this.type1Goods=response.data[1];
      	this.type2Goods=response.data[2];
      	this.type3Goods=response.data[3];
      })
      .catch(error=>{
      	alert("网络错误，不能访问")
      })

  },
  mounted:function(){
  	var orderHeight = document.body.clientHeight;
  	// console.log(orderHeight);
  	document.getElementById('order-list').style.height=orderHeight+'px';

  },
  methods:{
  	//添加商品方法
  	addOrderList(goods){
  		this.totalCount=0; //汇总数量清0
        this.totalMoney=0;
  		let isHave=false; //默认为不存在

  		for(let i=0;i<this.tableData.length;i++){
  			if(this.tableData[i].goodsId==goods.goodsId){
  				isHave=true; //存在
  			}
  		}
  		//如果存在的话
  		if(isHave){
  			let arr = this.tableData.filter(o=>o.goodsId==goods.goodsId);
  			arr[0].count++;
  		}else{
  			let newGoods={goodsId:goods.goodsId,goodsName:goods.goodsName,price:goods.price,count:1};
  			this.tableData.push(newGoods);
  		}
		this.getAllMoney();
    },
	//删除单个商品
    delSingleGoods(goods){
        console.log(goods);
        this.tableData=this.tableData.filter(o => o.goodsId !=goods.goodsId);
        this.getAllMoney();
    },
    //删除全部
    delAllGoods(){
		this.tableData = [];
		this.totalCount = 0;
		this.totalMoney = 0;
	},
	//计算属性
    getAllMoney(){
	    this.totalCount=0;
	    this.totalMoney=0;
	    if(this.tableData){
	        this.tableData.forEach((element) => {
	        this.totalCount+=element.count;
	        this.totalMoney=this.totalMoney+(element.price*element.count);   
	    	});
	    }
	}
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.pos-order{
	background-color: #f9fafc;
	border-right: 1px solid #c0ccda;
}
.div-btn{
	margin-top: 20px;
}
.title{
	height: 20px;
	border-bottom: 1px solid #D3DCE6;
	background-color: #F9FAFC;
	padding: 10px;
	text-align: left;
}
.often-goods-list ul li{
	list-style: none;
	float: left;
	border: 1px solid #E5E9F2;
	padding: 10px;
	margin:10px;
	/*text-align: left;*/
	background-color: #fff;
}
.o-price{
	color: #58B7FF;
}
.goods-type{
	/*float: left;*/
	clear: both;
	padding-left: 5px;
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
   }
   .cookList li span{
        display: block;
        float:left;
   }
   .foodImg{
       width: 40%;
       height:30px;   }
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
</style>

