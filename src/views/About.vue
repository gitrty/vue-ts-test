<template>
  <div class="about">
    <h1>about页面</h1>
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <div>{{msg}}</div>
  </div>
</template>

<script lang="ts">
import { Vue, Component } from "vue-property-decorator";
import HelloWorld from "@/components/HelloWorld.vue";

// 全局导航守卫改造
import router from "@/router";
router.beforeEach((to: any, from: any, next: any) => {
  // console.info(to);
  next();
});

// 装饰器 - 注册组件
@Component({
  components: {
    HelloWorld
  }
})

export default class About extends Vue {
  // private - 定义一个私有变量（等同于在vue的data中的变量）
  private msg: string = "私有变量msg";
}
</script>

<style scoped lang="less">
</style>