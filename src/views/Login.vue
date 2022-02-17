<template>
  <el-row type="flex" class="row-bg" justify="center">
    <el-col :xl="6" :lg="7">
      <div class="grid-content bg-purple">
        <h2>欢迎来到VueAdmin管理系统</h2>
        <el-image :src="require('@/assets/logo.png')" style="height: 180px;width: 180px"></el-image>
        <p>公众号----</p>
        <p>所有权----</p>
      </div>
    </el-col>
    <el-col :span="1">
      <el-divider direction="vertical"></el-divider>
    </el-col>
    <el-col :xl="6" :lg="7">
      <el-form :model="loginForm" :rules="rules" ref="loginForm" label-width="80px" class="loginForm">
        <el-form-item label="用户名" prop="username" style="width: 380px">
          <el-input v-model="loginForm.username"></el-input>
        </el-form-item>

        <el-form-item label="密码" prop="password"style="width: 380px">
          <el-input v-model="loginForm.password"></el-input>
        </el-form-item>
        <el-form-item label="验证码" prop="code"style="width: 380px">
          <el-input v-model="loginForm.code" style="width: 60%;float: left"></el-input>
          <el-image src="" class="captchaImg" style="width: 35%"></el-image>

        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="submitForm('loginForm')">登陆</el-button>
          <el-button @click="resetForm('loginForm')">重置</el-button>
        </el-form-item>
      </el-form>
    </el-col>
  </el-row>
</template>

<script>
export default {
  name: "login",
  data() {
    return {
      loginForm: {
        username: '',
        password: '',
        code: '',
        token:''
      },
      rules: {
        username: [
          {required: true, message: '请输入用户名', trigger: 'blur'},
        ],
        password: [
          {required: true, message: '请输入密码', trigger: 'blur'},
        ],
        code: [
          {required: true, message: '请输入验证码', trigger: 'blur'},
          {min: 5, max: 5, message: '长度为5 个字符', trigger: 'blur'}
        ],
      }
    };
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          this.$axios.post('/login',this.loginForm).then(
              res=>{

              }
          )
        } else {
          console.log('error submit!!');
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    }
  }
}
</script>

<style scoped>

.el-row{
  background-color: #42b983;
  height: 100%;
  /*width: 100%;*/
  display: flex;
  align-items: center;
  text-align: center;
  justify-content: center;
}
.el-divider{
  height: 200px;
}

.captchaImg{
float: left;
  margin-left: 8px;
  border-radius: 4px;
}
</style>
