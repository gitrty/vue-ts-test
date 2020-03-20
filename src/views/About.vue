<template>
  <div class="about">
    <h1>about页面</h1>
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <div>{{msg}}</div>
    <button @click="myFun({name:'toyo',age:18})">点击触发函数</button>
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

// 使用interface接口 - 接口要定义在装饰器上面 （项目中可将所有接口封装为一个模块，按需引入）
interface userInfoFace {
  name: string;
  age?: number;
}

// 装饰器 - 注册组件
@Component({
  components: {
    HelloWorld
  }
})
export default class About extends Vue {
  // private - 定义一个私有变量（等同于在vue的data中的变量）
  private msg: string = "私有变量msg";

  private myFun(userInfo: userInfoFace) {
    console.info(userInfo);
    // this.fn2({ name: "toyo", age: "123" });     // 此处age会红线，因为 userInfoFace接口 规定了需要number类型
  }

  fn2(userInfo: userInfoFace) {}
}
</script>

<style scoped lang="less">
</style>