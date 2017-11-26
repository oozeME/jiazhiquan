<template>
	<div>
		<el-tabs type="border-card">
			<el-tab-pane label="全部项目">
			</el-tab-pane>
			<el-tab-pane label="日常保洁" index></el-tab-pane>
			<el-tab-pane label="深度清洁"></el-tab-pane>
			<el-tab-pane label="保姆（到家做饭）"></el-tab-pane>
			<el-tab-pane label="月嫂/育儿嫂"></el-tab-pane>
			<el-tab-pane label="家居清洗"></el-tab-pane>
			<el-tab-pane label="周期保洁"></el-tab-pane>
			<el-tab-pane label="企业保洁"></el-tab-pane>
			<el-tab-pane label="代办跑腿"></el-tab-pane>
			<el-tab-pane label="家电清洗"></el-tab-pane>
			<el-tab-pane label="家庭安装及维修"></el-tab-pane>
	  </el-tabs>
	  <div class="navs">
		  <el-col :span="3">
		  	<div class="grid-content bg-purple-light">
			  <el-dropdown>
			  	<el-button type="primary">
				    选择城市<i class="el-icon-arrow-down el-icon--right"></i>
				  </el-button>
				  <el-dropdown-menu slot="dropdown">
				    <el-dropdown-item>黄金糕</el-dropdown-item>
				    <el-dropdown-item>狮子头</el-dropdown-item>
				    <el-dropdown-item>螺蛳粉</el-dropdown-item>
				    <el-dropdown-item>双皮奶</el-dropdown-item>
				    <el-dropdown-item>蚵仔煎</el-dropdown-item>
				  </el-dropdown-menu>
			  </el-dropdown>
			</div>
		  </el-col>
		  <el-col :span="7" align="right">
		  	<el-form :inline="true" :model="formInline" class="demo-form-inline">
				<el-input v-model="formInline.service" placeholder="查询服务"></el-input>
				  <el-button type="primary" @click="onSubmit">查询</el-button>
				</el-form>
		  </el-col>
		  <el-button @click="onFind">添加项目</el-button>
		</div>
		<el-table
	     :data="tableData"
	     border
	     style="width: 100%">
	     <el-table-column
	       prop="num"
	       label="排序号"
	       width="120%">
	     </el-table-column>
	     <el-table-column
	       prop="pic"
	       label="图片"
	       width="120%">
	     </el-table-column>
	     <el-table-column
	       prop="name"
	       label="项目名称"
	       width="120%">
	     </el-table-column>
	     <el-table-column
	       prop="price"
	       label="价格/单位"
	       width="120%">
	     </el-table-column>
	     <el-table-column
	       prop="instore"
	       label="店内分类"
	       width="120%">
	     </el-table-column>
	     <el-table-column
	       prop="terrace"
	       label="平台分类"
	       width="120%">
	     </el-table-column>
	     <el-table-column
	       prop="filters"
	       label="筛选项"
	       width="120%">
	     </el-table-column>
	     <el-table-column
	       prop="city"
	       label="城市"
	       width="120%">
	     </el-table-column>
	     <el-table-column
	       prop="status"
	       label="状态"
	       width="120%">
	     </el-table-column>
	     <el-table-column
	       prop="sales"
	       label="销量"
	       width="120%">
	     </el-table-column>
	     <el-table-column label="操作" >
	      <template slot-scope="scope">
	        <el-button
	          size="mini"
	          @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
	        <el-button
	          size="mini"
	          type="danger"
	          @click="handleDelete(scope.$index, scope.row)">删除</el-button>
	      </template>
	     </el-table-column> 
	    </el-table>
		
		
	</div>
</template>

<script>
   export default {
    data() {
      return {
      	modal1: false,
        formInline: {
          service: ''
        },
        tableData: [{
          num: 1,
          pic: '',
          name: '地暖清洗',
          price:"99元/个",
          oldprice:"￥120",
          instore:"家居清洗",
          terrace:"家具养护",
          filters:"iii",
          city:"城市",
          status:"上架",
          sales:11
          
        }, {
          num: 1,
          pic: '',
          name: '地暖清洗',
          price:"99元/个",
          oldprice:"￥120",
          instore:"家居清洗",
          terrace:"家具养护",
          filters:"",
          city:"城市",
          status:"上架",
          sales:11
        }, {
          num: 1,
          pic: '',
          name: '地暖清洗',
          price:"99元/个",
          oldprice:"￥120",
          instore:"家居清洗",
          terrace:"家具养护",
          filters:"",
          city:"城市",
          status:"上架",
          sales:11
        }, {
          num: 1,
          pic: '',
          name: '地暖清洗',
          price:"99元/个",
          oldprice:"￥120",
          instore:"家居清洗",
          terrace:"家具养护",
          filters:"",
          city:"城市",
          status:"上架",
          sales:11
        }]
      }
    },
    methods: {
       onSubmit() {
        console.log('submit!');
      },
      onFind(){
      	console.log(8888)
      },
      handleEdit(index, row) {
        console.log(index, row);
      },
      handleDelete(index, row) {
        console.log(index, row);
      }
    }
    
  };
</script>

<style>
.navs>*{
	height: 40px;
}
.el-tabs .el-tabs--border-card{
	height: 60px;
}.el-tabs__nav-next, .el-tabs__nav-prev{
	line-height: 60px;
}
.el-tabs--border-card>.el-tabs__header .el-tabs__item.is-active{
	height: 50px;
}
.el-tabs--border-card>.el-tabs__header{
	background: #f2f2f2;
	height: 60px;
	line-height: 60px;
}
.el-tabs__item.is-active{
	color: #111;
	font-weight: 600;
}
.el-tabs__item{
	color: #48576a;
}
.el-tabs--border-card>.el-tabs__content{
	padding:0;
}
.demo-form-inline{
	display: flex;
}
.demo-form-inline input{
	width:80%;
}
.demo-form-inline button{
	width:60px;
}
.el-table__header,.el-table__body{
	width:100%;
}
.el-button--default,.el-button--primary{
	background: #FFF;
	color: #999;
	border-color:#999;
	height:35px;
}
.el-button--default:hover,.el-button--primary:hover{
	background: #D1DBE5;
	border-color: #999;
	
}
.el-button--default{
	margin-left:30px;
}
.navs{
	height:40px;
	margin-top:10px;
}

.el-dropdown,.el-button--primary{
	width: 100%;
}
.marsk{
	position: fixed;
	width: 100%;
	height:100%;
	background: rgba(0,0,0,.4);
	z-index: 99999;
	top: 0;
	left: 0;
}

</style>