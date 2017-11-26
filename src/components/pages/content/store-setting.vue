<template>
    <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="140px" class="demo-ruleForm">
        <!-- 店铺名称 -->
        <el-form-item label="店铺名称" prop="name">
            <el-input v-model="ruleForm.name"></el-input>
        </el-form-item>
        <!-- 店铺相册 -->
        <el-form-item label="店铺相册">
            <el-upload
			  action="../../../assets"
			  list-type="picture-card"
			  :on-preview="handlePictureCardPreview"
			  :on-remove="handleRemove">
			  <i class="el-icon-plus"></i>
			</el-upload>
			<el-dialog :visible.sync="dialogVisible" size="tiny">
			  <img width="100%" :src="dialogImageUrl" alt="">
			</el-dialog>
        </el-form-item>
        <!-- 订购须知 -->
        <el-form-item label="订购须知">
            <el-input type="textarea" v-model="ruleForm.msg" :autosize="{ minRows: 2, maxRows: 10 }"></el-input>
        </el-form-item>
        <!-- 商家简介 -->
        <el-form-item label="商家简介">
            <el-input type="textarea" v-model="ruleForm.shop_info" :autosize="{ minRows: 2, maxRows: 10 }"></el-input>
        </el-form-item>
        <!-- 客服电话 -->
        <el-form-item label="客服电话">
            <el-input suffix-icon="el-icon-date" v-model="ruleForm.tel" class='inpwidth'>
            </el-input>
        </el-form-item>
        <!-- 服务时间 -->
        <el-form-item label="服务时间" required>
            <div class="block">
		    <el-date-picker
		      v-model="value1"
		      type="date"
		      placeholder="选择日期">
		    </el-date-picker>
		    至
		    <el-date-picker
		      v-model="value2"
		      type="date"
		      placeholder="选择日期">
		    </el-date-picker>
		  </div>
            <div class="day_box">
                <span class="active_day">周一</span>
                <span class="active_day">周二</span>
                <span class="active_day">周三</span>
                <span class="active_day">周四</span>
                <span class="active_day">周五</span>
                <span class="active_day">周六</span>
                <span class="active_day">周日</span>
                <span class="prompt">绿色表示营业时间，灰色表示休息时间</span>
            </div>
        </el-form-item>

        <el-form-item label="服务范围">
            <div class="area_box">
                <span class="area_item">眉山</span>
                <span class="area_item">北京</span>
                <span class="area_item">上海</span>
                <span class="area_item">深圳</span>
                <span class="area_item">广州</span>
                <span class="area_item">佛山</span>
                <span class="area_item">杭州</span>
                <span class="area_item">天津</span>
                <span class="area_item">长沙</span>
                <span class="area_item">成都</span>
                <span class="area_item">重庆</span>
                <span class="area_item">惠州</span>
                <span class="area_item">西安</span>
                <span class="area_item">苏州</span>
                <span class="area_item">南京</span>
                <span class="area_item">青岛</span>
                <span class="area_item">武汉</span>
                <span class="area_item refresh">刷新</span>
            </div>
        </el-form-item>
        <!-- 最低起购金额 -->
        <el-form-item label="最低起购金额">
            <el-input v-model="ruleForm.min_price" placeholder="满足最低起购金额方可服务（元）" class='inpwidth'></el-input>
        </el-form-item>
        <!-- 附加费 -->
        <el-form-item label="附加费">
            <el-input v-model="ruleForm.other_price" placeholder="上门费或其他额外费用（元）" class='inpwidth'></el-input>
        </el-form-item>
        <!-- 免附加费起购金额 -->
        <el-form-item label="免附加费起购金额">
            <el-input v-model="ruleForm.no_other_min_price" placeholder="上门费或其他额外费用（元）" class='inpwidth'></el-input>
        </el-form-item>
        <!-- 提前预约 -->
        <el-form-item label="提前预约">
            <el-input v-model="ruleForm.time" placeholder="用户预约时间须大于下单时间的间隔小时数，必须是0.5的整倍数（小时）" class='inpwidth'></el-input>
        </el-form-item>
        <!-- 使用上单小程序 -->
        <!--<el-form-item label="使用上单小程序" prop="delivery">
            <el-switch v-model="ruleForm.sd"></el-switch>
        </el-form-item>-->
        <!-- 使用抢单模式 -->
        <!--<el-form-item label="抢单模式" prop="delivery">
            <el-switch v-model="ruleForm.qd"></el-switch>
        </el-form-item>-->
        <!-- 保存 -->
        <el-form-item>
            <el-button type="primary" @click="submitForm('ruleForm')">保存</el-button>
        </el-form-item>
    </el-form>
</template>
<script>
	import uploader from './uploader.vue'
    export default {
        data() {
            return {
            	dialogImageUrl: '',
        		dialogVisible: false,
        		value1: '',
        		value2: '',
                ruleForm: {
                    name: '', //店铺名称
                    photos: '', //店铺相册
                    msg: '', //订购须知
                    shop_info: '', //商家简介
                    tel: '', //客服电话
                    start_time: '', //开始时间
                    end_time: '', //结束时间
                    no_other_min_price: '', //免附加费最低起购金额
                    min_price: '', //最低起购金额
                    other_price: '', //附加费
                    time: '', //提前预约时间
                    sd:'',//上单小程序
                    qd:'',//抢单模式
                    region: '',
                    date1: '',
                    date2: '',
                    delivery: false,
                    type: [],
                    resource: '',
                    desc: ''
                },
                rules: {
                    name: [{
                            required: true,
                            message: '请输入店铺名称',
                            trigger: 'blur'
                        },
                        {
                            min: 3,
                            max: 5,
                            message: '长度在 3 到 5 个字符',
                            trigger: 'blur'
                        }
                    ],
                    region: [{
                        required: true,
                        message: '请选择活动区域',
                        trigger: 'change'
                    }],
                    date1: [{
                        type: 'date',
                        required: true,
                        message: '请选择日期',
                        trigger: 'change'
                    }],
                    date2: [{
                        type: 'date',
                        required: true,
                        message: '请选择时间',
                        trigger: 'change'
                    }],
                    type: [{
                        type: 'array',
                        required: true,
                        message: '请至少选择一个活动性质',
                        trigger: 'change'
                    }],
                    resource: [{
                        required: true,
                        message: '请选择活动资源',
                        trigger: 'change'
                    }],
                    desc: [{
                        required: true,
                        message: '请输入商家简介',
                        trigger: 'blur'
                    }],
                    phone: [{
                        required: true,
                        message: '请输入客服电话',
                        trigger: 'blur'
                    }],
                    shop_info: [{
                        required: true,
                        message: '请输入商家简介',
                        trigger: 'blur'
                    }]
                },
		        value3: [new Date(), new Date()],
		        value4: ''
            };
        },
        beforeCreate(){
        	//页面加载之前请求数据
	    	var _this=this;
	    	var userid=parseInt(sessionStorage.getItem("userid")) ;
	    	var phone=sessionStorage.getItem("phone");
	    	console.log(userid,phone)
	    	this.axios.get("/home/api/getshopsetupinfo?userid="+userid+"&phone="+phone).then(function(data) {
	    		var datad=data.data.data;
	    		sessionStorage.setItem("userid",datad.userid);
	    		sessionStorage.setItem("id",datad.id);
	    		sessionStorage.setItem("phone",datad.phone);
	        	_this.ruleForm.time=datad.appointmenttime;
	        	_this.ruleForm.min_price=datad.attachcost;
	        	_this.ruleForm.other_price=datad.exemptattachcost;
	        	_this.ruleForm.no_other_min_price=datad.minorderlimit;
	        	_this.ruleForm.name=datad.name;
	        	_this.ruleForm.msg=datad.orderattention;
	        	_this.ruleForm.tel=datad.servicemobile;
				_this.value1=datad.servicetimebegin;
				_this.value2=datad.servicetimeend;
				_this.ruleForm.shop_info=datad.shopintro;
	        },function(){
	        	_this.$message.error('加载失败');
	        })
	    },
        components: {
        	//加载插件
			uploader
		},
        methods: {
        	//点击提交
            submitForm(formName) {
                this.$refs[formName].validate((valid) => {
                    if (valid) {
                        var _this=this;
				    	var userid=parseInt(sessionStorage.getItem("userid")) ;
				    	var phone=sessionStorage.getItem("phone");
				    	console.log(_this.value1,_this.value2)
				    	this.axios.post("/home/api/addshopsetupinfo", {
				    		userid:userid,
				            phone:phone,
				            name:_this.ruleForm.name,
				            album:"",
				            orderattention:_this.ruleForm.msg,
				            shopintro:_this.ruleForm.shop_info,
				            servicemobile:_this.ruleForm.tel,
				            servicetimebegin:_this.value1,
				            servicetimeend:_this.value2,
				            week:"",
				            servicerange:"",
				            minorderlimit:_this.ruleForm.no_other_min_price,
				            attachcost:_this.ruleForm.min_price,
				            exemptattachcost:_this.ruleForm.other_price,
				            appointmenttime:_this.ruleForm.time,
				        }).then(function(data) {
				        	console.log(data)
				        },function(){
				        	_this.$message.error('加载失败');
				        })
                    } else {
                        console.log('error submit!!');
                        return false;
                    }
                });
            },
            resetForm(formName) {
                this.$refs[formName].resetFields();
            },
            handleRemove(file, fileList) {
		      console.log(file, fileList);
		    },
		    handlePictureCardPreview(file) {
		      this.dialogImageUrl = file.url;
		      this.dialogVisible = true;
		        
		    }
        }
    }

</script>
<style scoped>
	.demo-ruleForm{
		padding-top:20px;
	}
    .day_box {
        margin-top: 50px;
    }

    .active_day {
        background: #21BA5C;
        color: #fff;
        margin-right: 12px;
        line-height: 30px;
        border-radius: 5px;
        display: inline-block;
        padding: 0 12px;
    }

    .active_day.no_active_day {
        background: #ccc;
        color: #fff;
    }

    .area_box {
        display: flex;
        flex-wrap: wrap;
    }

    .area_item {
        background: #115F88;
        color: #fff;
        margin-right: 12px;
        line-height: 30px;
        border-radius: 5px;
        display: inline-block;
        padding: 0 12px;
        margin-bottom: 12px;
    }
    
    .refresh {
        background: #21BA5C;
    }
    
    .area_item{
    	cursor: pointer;
    }
    
    .prompt{
    	color: #999;
    }
    
    .inpwidth{
    	width: 500px;
    }
</style>