<template>
  <div class="login">
    <div class="login-content">
      <nuxt-link class="link" to="/">
        <img src="@/assets/images/head-logo.png" alt="" />
      </nuxt-link>
      <a-form
        id="components-form-demo-normal-login"
        :form="form"
        class="login-form"
        @submit="handleSubmit"
      >
        <a-form-item>
          <a-input
            v-decorator="[
              'username',
              {
                rules: [
                  { required: true, message: 'Please input your username!' }
                ]
              }
            ]"
            placeholder="用户名"
          >
            <a-icon slot="prefix" type="user" style="color: rgba(0,0,0,.25)" />
          </a-input>
        </a-form-item>
        <a-form-item>
          <a-input
            v-decorator="[
              'password',
              {
                rules: [
                  { required: true, message: 'Please input your Password!' }
                ]
              }
            ]"
            type="password"
            placeholder="密码"
          >
            <a-icon slot="prefix" type="lock" style="color: rgba(0,0,0,.25)" />
          </a-input>
        </a-form-item>
        <a-form-item>
          <a-checkbox
            v-decorator="[
              'remember',
              {
                valuePropName: 'checked',
                initialValue: true
              }
            ]"
            >记住账号</a-checkbox
          >
          <a class="login-form-forgot" href>忘记密码</a>
          <a-button type="primary" html-type="submit" class="login-form-button"
            >登录</a-button
          >
        </a-form-item>
      </a-form>
      <button @click="handleSubmit">denglu</button>
    </div>
  </div>
</template>

<script>
export default {
  beforeCreate() {
    this.form = this.$form.createForm(this, { name: "normal_login" });
  },
  methods: {
    handleSubmit(e) {
      e.preventDefault();
      // this.$router.push("/");
      this.form.validateFields((err, values) => {
        if (!err) {
          let {username,password} = values
          this.$axios.post(`api/login`,{username,password}).then(res => {
            console.log(res);
            
          });
        }
      });
    }
  }
};
</script>
<style>
.login {
  width: 100%;
  height: 100vh;
  background: url("../assets/images/reg_bg.jpg");
  background-size: auto 100vh;
  position: relative;
}
.login-content {
  background-color: #ffffff;
  width: 460px;
  left: 50%;
  margin-left: -230px;
  border-radius: 20px;
  box-shadow: 0 0 30px rgba(0, 0, 0, 0.1);
  padding: 65px 0 30px 0;
  position: fixed;
  top: 15%;
  padding: 80px 40px 20px 40px;
}
.link img {
  position: absolute;
  top: -60px;
  left: 101px;
  width: 258px;
  height: 120px;
}
#components-form-demo-normal-login .login-form {
  max-width: 300px;
}
#components-form-demo-normal-login .login-form-forgot {
  float: right;
}
#components-form-demo-normal-login .login-form-button {
  width: 100%;
}
</style>
