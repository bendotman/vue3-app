<template>
  <div>
    <h3>Simple Calculator</h3>
    <form>
      <input type="text" @keyup="addNumbers" v-model="num1" />
      <span>+</span>
      <input type="text" @keyup="addNumbers" v-model="num2" />
      <span>=</span>
      <span>{{result}}</span>
    </form>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  name: "Calculator",

  // setup은 하나의 vue객체의 변수와 메소드를 모두 포함하고있는 상태값이다.
  setup() {
    // ref를 사용하여 변수를 선언하면 각 변수는 value라는 값을 갖는다.
    let num1 = ref(0);
    let num2 = ref(0);
    let result = ref(0);

    // vue2에서 methods안에 fucntion을 선언했지만 vue3 에서는 setup에 모두 선언하고 return하면 된다.
    function addNumbers() {
      result.value = parseInt(num1.value) + parseInt(num2.value);
    }

    return {
      num1,
      num2,
      result,
      addNumbers,
    };
  },
};
</script>

<style>
</style>