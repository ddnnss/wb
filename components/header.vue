<template>
  <header class="header">
    <div class="container">
         <div class="header-top">
      <div class="header-top__logo">
        <p class="header-top__logo-p1"> <nuxt-link to="/"><span class="color-dark">LIDER</span>.PRESS</nuxt-link>  </p>
        <p class="header-top__logo-p2 color-dark mobile-hide"> Портал по борьбе с инфоцыганством</p>
      </div>
      <div class="header-top__links mobile-hide">
        <el-link :underline="false" href="https://element.eleme.io" class="text-bold color-dark" target="_blank">VK</el-link>
        <el-link :underline="false" href="https://element.eleme.io" class="text-bold color-dark" target="_blank">INSTA</el-link>
        <el-link :underline="false" href="https://element.eleme.io" class="text-bold color-dark" target="_blank">FACEBOOK</el-link>
      </div>
        <el-button @click="drawer=true" class="mobile-show" type="info" icon="el-icon-menu" plain></el-button>
    </div>
  <el-menu :router="true" :default-active="activeIndex" class="el-menu-demo mobile-hide" mode="horizontal">
  <el-menu-item class="menu-item" :route="{path:'/'}" index="1">Главная</el-menu-item>
  <el-menu-item class="menu-item" route="/list" index="2">Черный список</el-menu-item>
  <el-menu-item class="menu-item" route="/posts" index="3">статьи</el-menu-item>
  <el-menu-item class="menu-item" :route="{path:'/'}" index="4">обратная связь</el-menu-item>
  <el-menu-item class="menu-item" :route="{path:'/'}" index="5">о нашем сайте</el-menu-item>



</el-menu>
<div class="line"></div>

    </div>

<el-drawer
  size="70%"
  :visible.sync="drawer"
  :with-header="false">

  <div style="padding: 20px 40px">
    <div class="header-top__logo mb25">
        <p class="header-top__logo-p1"> <nuxt-link to="/"><span class="color-dark">LIDER</span>.PRESS</nuxt-link>  </p>

      </div>

  <ul>
    <li><nuxt-link to="/" class="text-up text-bold mb10">Главная</nuxt-link></li>
    <li><nuxt-link to="/list" class="text-up text-bold mb10">Черный список</nuxt-link></li>
    <li><nuxt-link to="/posts" class="text-up text-bold mb10">статьи</nuxt-link></li>
    <li><nuxt-link to="/" class="text-up text-bold mb10">обратная связь</nuxt-link></li>
    <li><nuxt-link to="/" class="text-up text-bold mb10">о нашем сайте</nuxt-link></li>
  </ul>
  </div>


</el-drawer>


  </header><!--header-->
</template>

<script>
  export default {
    data() {
      return {
        activeIndex: '1',
        drawer: false,
      };
    }
  };
</script>
