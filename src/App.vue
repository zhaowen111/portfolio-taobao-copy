<script setup>
import DropDownSelector from "./components/DropDownSelector/DropdownSelector.vue"
import arrowUp from "./assets/buycart.svg?no-inline";
const testOptions = [{ text: "我的淘宝", link: "www.baidu.com" }, { text: "我的足迹", link: "www.baidu.com" }, { text: "我的卡卷包", link: "www.baidu.com" }]
alert(window.innerWidth);
</script>

<template>
  <div class="design"></div>
  <div class="container">
  <!-- header section -->
    <header>
      
      <!-- 菜单栏 -->
      <nav>
        <DropDownSelector :options="testOptions" :icon="arrowUp"></DropDownSelector>
      </nav>
      
      <!-- 搜索栏 -->
      <div></div>
    
    </header>
    <!-- 侧边栏导航 -->
    <aside>
      <nav></nav>
    </aside>
    <!-- 网页主体部分 -->
    <main>
      <!-- 分类 -->
      <div></div>

      <!-- 商品列表 -->
      <div></div>
    </main>
    
    <footer>
      <!-- 淘宝网介绍 -->
      <div></div>
    
      <!-- 相关链接 -->
      <div></div>

      <!-- 法律声明 -->
      <div></div>
    </footer>
  </div>
  
</template>

<style scoped lang="scss">
.container {}

.design {
  position: absolute;
  left: 0;
  top: 0;
  width: 1536px;
  height: 100vh;
  background-image: url("./assets/design.png");
  background-size: contain;
  background-repeat: no-repeat;
  opacity: 0.3;
}

header nav {
  height: 35px;
  box-sizing: border-box;
  display: flex;
  align-items: center;
}
</style>
