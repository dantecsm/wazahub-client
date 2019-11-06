<template>
  <header :class="{'login': isLogin, 'no-login': !isLogin}">
    <template v-if="!isLogin">
      <h1><router-link to="/">WazaHub</router-link></h1>
      <p>每日一技</p>
      <div class="btns" v-if="$route.path!=='/login' && $route.path!=='/register'">
        <router-link to="/login"><el-button>立即登录</el-button></router-link>
        <router-link to="/register"><el-button>注册账号</el-button></router-link>
      </div>
    </template>

    <template v-if="isLogin">
      <h1><router-link to="/">Let's share</router-link></h1>
      <router-link to="/create"><i class="edit el-icon-plus"></i></router-link>
      <div class="user">
        <img :src="user.avatar" :alt="user.username" :title="user.username" class="avatar">
        <ul>
          <li><router-link to="/my">我的</router-link></li>
          <li><a href="#" @click="logout">注销</a></li>
        </ul>        
      </div>
    </template>
  </header>
</template>

<style lang="less" scoped>
  @import "../assets/base.less";

  header.no-login {
    padding: 0 12% 30px 12%;
    background: @bgColor;
    display: grid;
    justify-items: center;

    h1 {
      font-size: 40px;
      margin: 60px 0 0 0;

      a {
        color: #fff;
      }
    }

    p {
      margin: 15px 0 0 0;
      color: #fff;
    }

    button {
      margin: 20px 5px 0;
    }

    .btns {
      margin-top: 20px;
    }
  }

  header.login {
    display: flex;
    align-items: center;
    background: @bgColor;

    h1 {
      margin: 0;
      padding: 0;
      font-size: 40px;
      text-transform: uppercase;
      flex: 1;

      a {
        color: #fff;
      }
    }

    .edit {
      color: #fff;
      font-size: 30px;
    }

    .avatar {
      width: 40px;
      height: 40px;
      border: 1px solid #fff;
      border-radius: 50%;
      margin-left: 15px;
    }

    .user {
      position: relative;

      &:hover ul {
        display: block;
      }

      ul {
        display: none;
        position: absolute;
        right: 0;
        list-style: none;
        border: 1px solid #eaeaea;
        margin: 0;
        padding: 0;
        background-color: #fff;
      }

      a {
        text-decoration: none;
        color: #333;
        font-size: 12px;
        display: block;
        padding: 5px 10px;

        &:hover {
          background-color: #eaeaea;
        }
      }
    }
  }
</style>

<script>

  
  import { mapGetters, mapActions } from 'vuex'

  export default {
    data() {
      return {}
    },

    computed: {
      ...mapGetters([
        'isLogin',
        'user'
        ])
    },

    created() {
      this.checkLogin()
    },

    methods: {
      ...mapActions([
        'checkLogin',
        'logout'
        ])
    }
  }
</script>