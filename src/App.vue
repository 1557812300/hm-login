<template>
  <div id="app">
    <el-card class="login-card">
      <el-form
        style="margin-top: 50px"
        :model="loginForm"
        :rules="loginRuls"
        ref="loginForm"
      >
        <el-form-item prop="mobile">
          <el-input
            v-model="loginForm.mobile"
            placeholder="请输入您的手机号"
            type="text"
          ></el-input>
        </el-form-item>
        <el-form-item prop="password">
          <el-input
            v-model="loginForm.password"
            placeholder="请输入您的密码"
            type="password"
          ></el-input>
        </el-form-item>
        <el-form-item>
          <el-button class="button" type="primary" @click="login()"
            >登录</el-button
          >
        </el-form-item>
      </el-form>
    </el-card>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    const checkMobile = function (rule, value, callback) {
      //校验的是value
      //第三位必须是9
      value.charAt(2) === "9"
        ? callback()
        : callback(new Error("手机号第三位必须是9"));
    };
    return {
      //数据对象
      loginForm: {
        //检验的字段
        mobile: "",
        password: "",
      },
      //检验规则
      // {key:value}
      loginRuls: {
        mobile: [
          { required: true, message: "手机号不能为空", taigger: "blur" },
          {
            message: "手机号格式不正确",
            pattern: /^1[3-9]\d{9}$/, //手机号校验格式
            taigger: "blur",
          },
          {
            tragger: "blur",
            validator: checkMobile,
          },
        ],
        password: [
          { required: true, message: "密码不能为空", tragger: "blur" },
          {
            min: 6,
            max: 16,
            tragger: "blur",
            message: "密码长度为6-16位",
          },
        ],
      },
      }
    },
    methods: {
        login () {
          // then是成功校验
          // catch是失败校验
          this.$refs.loginForm.validate().then(()=>{
            console.log('打印成功')
          }).catch(()=>{
            console.log('打印失败')
          })
          }
        }
  }
</script>

<style>
/* vh可视屏的100% */
#app {
  width: 100%;
  height: 100vh;
  background-color: aquamarine;
  display: flex;
  justify-content: center;
}
.login-card {
  margin-top: 200px;
  width: 400px;
  height: 300px;
}
.a1 {
  width: 400px;
  height: 300px;
  background-color: #fff;
}
.button {
  margin: auto;
  width: 100%;
}
</style>
