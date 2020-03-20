<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" @click="clickPhoto" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <div>私有变量：{{msg}}</div>
    <div>计算属性：{{computedMsg}}</div>
  </div>
</template>


<script lang='ts'>
// lang = 'ts' 注意设定
import { Vue, Component } from "vue-property-decorator";
import HelloWorld from "@/components/HelloWorld.vue";

// 注册组件
@Component({
  components: {
    HelloWorld
  }
})
export default class Home extends Vue {
  // 定义私有变量
  private msg: number = 100;

  // 生命周期函数
  private mounted() {
    console.info("mounted生命周期");
  }

  // computed 计算属性
  private get computedMsg() {
    return "computed" + this.msg * 2;
  }

  // method 定义函数
  private clickPhoto() {
    alert(`点击图片触发了 clickPhoto 函数`);
  }
}
</script>
