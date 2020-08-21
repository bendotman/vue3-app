<template>
  <div>
    <h3>Simple Calculator</h3>
    <form>
      <input type="text" v-model="state.num1" />
      <span>+</span>
      <input type="text" v-model="state.num2" />
      <span>=</span>
      <span>{{state.result}}</span>
    </form>
  </div>
</template>

<script>
import { reactive, computed } from "vue";
export default {
  name: "Calculator",

  // setup은 하나의 vue객체의 변수와 메소드를 모두 포함하고있는 상태값이다.
  setup() {
    // reactive를 사용하면 하나의 vue객체의 변수들에 state속성을 주입한다.
    // state속성을 주입하면 vue에서 참조하여 사용할 수 있다.
    let state = reactive({
      num1: 0,
      num2: 0,
      // computed를 사용하면 template에서 이벤트가 일어날때 메소드를 사용하지 않고 값이 변경됨에 따라 연산할 수 있다.
      // input은 이미 이벤트를 가지고있기 때문에 따로 선언할 필요 없이 computed를 사용하여 input이벤트를 리스닝할 수 있다.
      result: computed(() => parseInt(state.num1) + parseInt(state.num2)),
    });

    return {
      state,
    };
  },
};
</script>

<style>
</style>