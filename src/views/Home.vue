<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" @click="clickPhoto" />
    <HelloWorld :msg="propsMsg" :title="title" @emit-data="fatherFn" />
    <div>私有变量：{{msg}}</div>
    <div>计算属性：{{computedMsg}}</div>
    <button @click="promiseFun">触发执行Primose的函数</button>
  </div>
</template>


<script lang='ts'>
// lang = 'ts' 注意设定
import { Vue, Component, Watch } from "vue-property-decorator";
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
  private mounted(): void {
    console.info("mounted生命周期");
  }

  // computed 计算属性
  private get computedMsg(): string {
    return "computed" + this.msg;
  }

  // method 定义函数
  private clickPhoto(): any {
    this.msg = this.msg * 2;
    alert(`点击图片触发了 clickPhoto 函数,msg值*2`);
  }

  private propsMsg: string = "propsMsg的值";

  private title: string = "我是标题";

  // 子组件emit传过来的值
  private fatherFn(value: string) {
    console.info(value);
  }

  // watch 监听 - 当msg有变动时，触发后面的函数  （开启深度监听）
  // immediate - 首次绑定监听时不会触发函数，开始 immediate 后首次绑定也会触发函数
  @Watch("msg", { deep: true, immediate: true }) private watchMsg(
    newVal: number,
    oldVal: number
  ) {
    console.info(newVal, oldVal);
  }

  // 在函数中执行 Promise，并指定返回值类型
  private async promiseFun(): Promise<void> {
    const data = await new Promise((res, rej) => {
      res("Promise数据");
    });
    console.info(data);
  }
}
</script>
