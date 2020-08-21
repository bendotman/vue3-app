<template>
  <div class="hello">
    <div v-if="error">{{error}}</div>
    <!-- async로 호출되는 setup()을 쓰는 자녀 객체는 다음과 같이 suspense를 걸어준다. -->
    <Suspense v-else>
      <!-- 
        - suspense가 사용될 때는 응답이 오는 동안 로딩상태를 표시할 수 있다.
        - #default template에 응답 후에 보여질 컴포넌트를 넣고, 
        - #fallback template에 로딩시 보여질 상태를 넣는다. 
      -->
      <template #default>
        <users />
      </template>
      <template #fallback>
        <div>Loading your amazing vuesers...</div>
      </template>
    </Suspense>
  </div>
</template>

<script>
import Users from "./sample02/Users.vue";
import { onErrorCaptured, ref } from "vue";

export default {
  name: "HelloWorld",
  setup() {
    const error = ref(null);

    onErrorCaptured((e) => {
      error.value = e;
    });

    return {
      error,
    };
  },

  components: {
    Users,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
