<template>
  <div>
    
    <Header></Header>
    <!-- 我是根组件 -->
    <!-- 路由组件出口的地方 -->
    <router-view></router-view>
    <!-- 在Home、Search下显示的  在登录、注册时隐藏 -->
    <!-- <Footer v-show="$route.path=='/home' || $route.path=='/search'"></Footer> -->
    <!-- 以上方法如果很多组件，就不合适了 -->
    <Footer v-show="$route.meta.show"></Footer>
  </div>
</template>

<script>
//引入 
import Header from './components/Header'
import Footer from './components/Footer'


export default {
  name: "App",
  components: {
    //注册 一定要记住  不然无法使用
    // <!-- KV一致省略V  -->
    Header,Footer
  }
};
</script>

<style scoped>
</style>
