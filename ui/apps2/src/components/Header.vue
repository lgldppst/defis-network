<template>
  <div class="header flexb">
    <div @click="handleToIndex"><img class="logo" src="@/assets/img/dex/logo.svg"></div>
    <div class="tools flexb">
      <!-- <label v-if="!scatter.identity" class="login" @click="handleLogin">{{ $t('public.login') }}</label>
      <label v-else class="account flexa">
        <span class="flexc iconSpan"><img width="100%" src="@/assets/img/dex/user_icon.svg" alt=""></span>
        <span>{{ scatter.identity.accounts[0].name }}</span>
      </label> -->
      <span class="create flexc" @click="handleToVote">{{ $t('vote.vote') }}</span>
      <span class="create flexc" @click="handleTo('farms')">{{ $t('farms.farms') }}</span>
      <span class="create flexc" @click="handleToPddex('pddex')">Pddex</span>
      <!-- <span class="create" @click="handleToCreate">{{ $t('dex.addMarket') }}</span> -->
      <span class="flexc" @click="listenShowTools"><img class="svgIcon" src="@/assets/img/dex/setup_icon.svg" alt=""></span>
      <span class="flexc" @click="handleShowNav"><img class="svgIcon" src="@/assets/img/dex/menu_icon.svg" alt=""></span>
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex';
import { login } from '@/utils/public';
export default {
  name: 'headerTools',
  computed: {
    ...mapState({
      // 箭头函数可使代码更简练
      scatter: state => state.app.scatter,
    }),
  },
  methods: {
    // 登录
    handleLogin() {
      login(this, () => {})
    },
    handleToIndex() {
      if (this.$route.name === 'index') {
        return
      }
      this.$router.push({name: 'index'})
    },
    handleShowNav() {
      this.$emit('listenShowNav', false)
    },
    listenShowTools() {
      this.$emit('listenShowTools', false)
    },
    handleToCreate() {
      this.$router.push({name: 'createMarket'})
    },
    handleTo(name) {
      if (this.$route.name === name)  {
        return;
      }
      this.$router.push({name: name})
    },
    handleToVote() {
      if (this.$route.name === 'vote') {
        return
      }
      this.$router.push({name: 'vote'})
    },
    handleToPddex() {
      location.href = 'https://pddex.defis.network/'
    }
  },
}
</script>

<style lang="scss" scoped>
.header{
  background: $color-bgcolor;
  height: 120px;
  padding: 0 40px;
  font-size: 28px;
  color: $color-tip;
  margin-bottom: 5px;
  .logo{
    width: 196px;
  }
  img{
    display: block;
  }
  .tools{
    .login{
      padding-right: 10px;
      color: $color-main;
      font-weight: 500;
    }
    .account{
      padding-right: 10px;
      color: #000;
      .iconSpan{
        width: 26px;
        margin-right: 12px;
      }
    }
    &>span{
      margin-left: 10px;
      height: 80px;
      min-width: 80px;
      background: $color-bgcolor;
      border-radius: 30px;
      box-shadow: 0px 20px 40px 0px rgba(220,220,220,0.5);
    }
    .create{
      box-sizing: border-box;
      box-shadow: none;
      padding: 10px;
      color: #000;
      margin-left: 00px;
    }
    .svgIcon{
      width: 30px;
    }
  }
}
</style>