<template>
  <div class="login-wap">
    <el-form class="login-form" label-position="top" label-width="80px" :model="formData">
      <h2>用户登陆</h2>
      <el-form-item label="用户名">
        <el-input v-model="formData.username"></el-input>
      </el-form-item>
      <el-form-item label="密码">
        <el-input type="password" v-model="formData.password" @keyup.enter.native="login()"></el-input>
        <!--  @keyup.enter.native="login() 可以回车直接登陆 -->
      </el-form-item>
      <el-button @click="login()" class="login-btn" type="primary" round>登陆</el-button>
    </el-form>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        formData: {
          username: '',
          password: ''
        }
      };
    },
    methods: {
      async login() {
        const res = await this.$axios.post('login', this.formData);
        const { data: { data, meta: { msg, status } } } = res;
        if (status === 200) {
          // console.log(data.id);
          // this.$router.push({ name: 'home', params: { userId: data.id } });
          this.$router.push('index');
          localStorage.setItem('userid', data.id);
          localStorage.setItem('token', data.token);
          // console.log(data.id);
          // console.log(localStorage.getItem('userid'));
        } else {
          this.$message.error(msg)
        }

      }
    },
  }
</script>
<style>
  .login-wap {
    background-color: #2c3e50;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
  }

  .login-form {
    background-color: #fff;
    width: 400px;
    height: 300px;
    margin: 100px auto;
    padding: 40px;
    border-radius: 10px;

  }

  .login-btn {
    width: 100%;
  }

  h2 {
    font-size: 20px;
    color: black;
  }
</style>
