<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h3>{{title}}</h3>
    <button @click="emitData">@Emit - 点击传值给父组件</button>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue, Emit } from "vue-property-decorator";

@Component
export default class HelloWorld extends Vue {
  // 从父组件接收的值
  @Prop() private msg!: string;

  // 接收父组件的值 - 带高级选项
  @Prop({
    required: false, // 是否必传
    default: "默认标题"
  })
  private title!: string; // ! 表示为非 null 或 undefined

  private sonData: string = "我是子组件的变量";

  // 点击事件的函数 - 父组件中通过 @emit-data="函数" 来接收，函数的参数就是return出的值
  @Emit() private emitData(): string {
    return this.sonData;
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
