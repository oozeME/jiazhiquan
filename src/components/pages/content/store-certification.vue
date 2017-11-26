<template>
	<el-form :model="ruleForm1" :rules="rules" ref="ruleForm1" label-width="140px" class="demo-ruleForm1">
	  <h3>企业基础信息</h3>
	  <el-form-item label="营业执照名称" prop="gszz">
	    <el-input v-model="ruleForm1.gszz"></el-input>
	  </el-form-item>
	  <el-form-item label="选择主体类型" prop="region">
	    <el-select v-model="ruleForm1.region" placeholder="选择主体类型">
	      <el-option label="公司" value="公司"></el-option>
	      <el-option label="个人" value="个人"></el-option>
	    </el-select>
	  </el-form-item>
	  <el-form-item label="营业执照扫描图" prop="gszzchart">
		<el-upload
		  action="https://jsonplaceholder.typicode.com/posts/"
		  list-type="picture-card"
		  :on-preview="handlePictureCardPreview"
		  :on-remove="handleRemove">
		  <i class="el-icon-plus"></i>
		</el-upload>
		<el-dialog :visible.sync="dialogVisible" size="tiny">
		  <img width="100%" :src="dialogImageUrl" alt="">
		</el-dialog>
	  </el-form-item>
	  <el-form-item label="统一社会信用代码" prop="credit">
	    <el-input v-model="ruleForm1.credit"></el-input>
	  </el-form-item>
	  <el-form-item label="营业执照注册号" prop="registration">
	    <el-input v-model="ruleForm1.registration"></el-input>
	  </el-form-item>
	  <el-form-item label="注册地址" prop="address">
	    <el-input v-model="ruleForm1.address"></el-input>
	  </el-form-item>
	  <el-form-item label="营业执照所在地" prop="seat">
	    <el-select v-model="ruleForm1.seat" placeholder="营业执照所在地">
	      <el-option label="上海" value="上海"></el-option>
	      <el-option label="北京" value="北京"></el-option>
	    </el-select>
	    <el-select v-model="ruleForm1.seat1" placeholder="区域">
	      <el-option label="昌平" value="昌平"></el-option>
	      <el-option label="回龙观" value="回龙观"></el-option>
	    </el-select>
	  </el-form-item>
	  <el-form-item label="法定代表人" prop="representative">
	    <el-input v-model="ruleForm1.representative"></el-input>
	  </el-form-item>
	   <el-form-item label="营业期限">
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
	  </el-form-item>
	  <h3>商家指定联系人信息</h3>
	  <el-form-item label="联系人身份证照片" prop="playname">
	    <el-upload
		  action="https://jsonplaceholder.typicode.com/posts/"
		  list-type="picture-card"
		  :on-preview="handlePictureCardPreview1"
		  :on-remove="handleRemove1">
		  <i class="el-icon-plus"></i>
		</el-upload>
		<el-dialog :visible.sync="dialogVisible1" size="tiny">
		  <img width="100%" :src="dialogImageUrl1" alt="">
		</el-dialog>
	  </el-form-item>
	  <el-form-item label="制定联系人姓名" prop="linkman">
	    <el-input v-model="ruleForm1.linkman"></el-input>
	  </el-form-item>
	  <el-form-item label="联系人身份证号码" prop="idcard">
	    <el-input v-model="ruleForm1.idcard"></el-input>
	  </el-form-item>
	  <el-form-item>
        <el-button type="primary" @click="submitForm('ruleForm1')">保存</el-button>
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
        dialogImageUrl1: '',
        dialogVisible1: false,
      	imageUrl: '',
        ruleForm1: {
          gszz: '',
          region: '',
          credit: '',
          registration :'',
          address :'',
          subjectStyle :'',
          seat :'',
          seat1 :'',
          representative :'',
          linkman :'',
          idcard: '',
          date1: '',
          date2: '',
          deadline:'',
          delivery: false
        },
        form:{
        	date1:"",
        	date2:""
        },
        value1:'',
        value2:'',
        value3: [new Date(), new Date()],
		value4: '',
        rules: {
          gszz: [
            { required: true, message: '请输入店铺名称', trigger: 'blur' },
            { min: 3, max: 40, message: '长度在 3 到 40 个字符', trigger: 'blur' }
          ],
          region: [
            { required: true, message: '请选择活动区域', trigger: 'change' }
          ],
          date1: [
            { type: 'date', required: true, message: '请选择日期', trigger: 'change' }
          ],
          date2: [
            { type: 'date', required: true, message: '请选择时间', trigger: 'change' }
          ],
          type: [
            { type: 'array', required: true, message: '请至少选择一个活动性质', trigger: 'change' }
          ],
          resource: [
            { required: true, message: '请选择活动资源', trigger: 'change' }
          ],
          desc: [
            { required: true, message: '请填写活动形式', trigger: 'blur' }
          ],
          address:[
          	{required:true,message:"请输入注册地址",trigger:'blur'}
          ],
          seat:[
          	{required:true,message:"请选择区域",trigger:'blur'}
          ],
          seat1:[
          	{required:true,message:"请选择区域",trigger:'blur'}
          ],
          representative:[
          	{required:true,message:"请输入法定代表人",trigger:'blur'}
          ],
          deadline:[
          	{required:true,message:"请选择营业期限",trigger:'blur'}
          ],
          representative:[
          	{required:true,message:"请输入注册地址",trigger:'blur'}
          ],
          linkman:[
          	{required:true,message:"请输入联系人姓名",trigger:'blur'}
          ],
          idcard:[
          	{required:true,message:"请输入联系人身份证号码",trigger:'blur'}
          ]
        }
      }
    },
    beforeCreate(){
    	var _this=this;
    	var userid=parseInt(sessionStorage.getItem("userid")) ;
    	var phone=sessionStorage.getItem("phone");
    	this.axios.get("/home/api/getshopcertifyInfo?userid="+userid+"&phone="+phone).then(function(data) {
        		var datad=data.data.data;
	    		sessionStorage.setItem("userid",datad.userid);
	    		sessionStorage.setItem("id",datad.id);
	    		sessionStorage.setItem("phone",datad.phone);
	    		
				if(datad.type==0){
		    		var type="公司";
		    	}else{
		    		var type="个人";
		    	}
		    	console.log(datad)
	            _this.ruleForm1.gszz=datad.licencename;
	            _this.ruleForm1.region=type;
	            _this.ruleForm1.credit=datad.creditcode;
	            _this.ruleForm1.registration=datad.licenceregnum;
	            _this.ruleForm1.address=datad.registaddress;
	            _this.ruleForm1.seat=datad.licencelocation;
	            _this.ruleForm1.representative=datad.legalentity;
	            _this.value1=datad.limittimebegin;
	            _this.value2=datad.limittimeend;
	            _this.ruleForm1.linkman=datad.name;
	            _this.ruleForm1.idcard=datad.identitycardnum;
        },function(){
        	_this.$message.error('加载失败');
        })
    },
    components: {
		uploader
	},
    methods: {
      submitForm(formName) {
        this.$refs[formName].validate((valid) => {
          if (valid) {
          	var _this=this;
	    	var userid=parseInt(sessionStorage.getItem("userid")) ;
	    	var phone=sessionStorage.getItem("phone");
	    	console.log(userid,phone)
	    	if(formName.region=="公司"){
	    		var type=0;
	    	}else{
	    		var type=1;
	    	}
	    	console.log(_this.ruleForm1.address)
	    	this.axios.post("/home/api/addshopcertifyInfo", {
	            userid: userid,
	            phone:phone,
	            licencename:_this.ruleForm1.gszz,
	            type:type,
	            licenceurl:"",
	            creditcode:_this.ruleForm1.credit,
	            licenceregnum:_this.ruleForm1.registration,
	            registaddress:_this.ruleForm1.address,
	            licencelocation:_this.ruleForm1.seat,
	            legalentity:_this.ruleForm1.representative,
	            limittimebegin:_this.value1,
	            limittimeend:_this.value2,
	            identitycardphoto:"",
	            name:_this.ruleForm1.linkman,
	            identitycardnum:_this.ruleForm1.idcard
	        }).then(function(data) {
	        	_this.$message.success('保存成功');
	        },function(){
	        	_this.$message.error('保存失败');
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
      handleAvatarSuccess(res, file) {
        this.imageUrl = URL.createObjectURL(file.raw);
      },
      handleRemove(file, fileList) {
        console.log(file, fileList);
      },
      handlePictureCardPreview(file) {
        this.dialogImageUrl = file.url;
        this.dialogVisible = true;
        
      },
      handleRemove1(file, fileList) {
        console.log(file, fileList);
      },
      handlePictureCardPreview1(file) {
        this.dialogImageUrl = file.url;
        this.dialogVisible = true;
        
      }
    }
  }
</script>

<style>
	.demo-ruleForm1{
		margin: 20px 0 0 20px;
	}
  .avatar-uploader .el-upload {
    border: 1px dashed #d9d9d9;
    border-radius: 6px;
    cursor: pointer;
    position: relative;
    overflow: hidden;
  }
  .avatar-uploader .el-upload:hover {
    border-color: #409EFF;
  }
  .avatar-uploader-icon {
    font-size: 28px;
    color: #8c939d;
    width: 100px;
    height: 100px;
    line-height: 100px;
    text-align: center;
  }
  .avatar {
    width: 100px;
    height: 100px;
    display: block;
  }
  h3{
  	line-height: 40px;
  	margin-left: 15px;
  
  }
</style>