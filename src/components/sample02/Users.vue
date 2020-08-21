<template>
  <div v-if="error">{{error}}</div>

  <AsyncUser
    v-for="user in users.data"
    :key="user.id"
    :user="user"
  >{{user.first_name}} {{user.last_name}}</AsyncUser>

  <!-- 정적 컴포넌트 -->
  <!-- <user
    v-for="user in users.data"
    :key="user.id"
    :user="user"
  >{{user.first_name}} {{user.last_name}}</user>-->
</template>

<script>
import { ref, defineAsyncComponent } from "vue";
// import User from "./User"; 정적으로 컴포넌트를 로드한다.
import Loading from "./Loading";

/**
 * webpackChunkName
 * 코드가 웹팩에 의해 스플리트될 때 호출된 파일의 이름을 붙여주는 기능
 */
const AsyncUser = defineAsyncComponent({
  loader: () => import("./User" /* webpackChunkName: "user" */),
  loadingComponent: Loading, // 로딩시 사용되는 컴포넌트 <Suspense>가 정의 되어있어야 동작한다.
  delay: 200,
  suspensible: false,
});

export default {
  name: "Users",

  async setup() {
    const error = ref(null);
    const users = ref(null);

    try {
      const usersResponse = await fetch("https://reqres.in/api/users");
      users.value = await usersResponse.json();
    } catch (e) {
      error.value = e;
    }

    return { users, error };
  },

  components: {
    /*
     * Synchronous Components
     * 어플리케이션 번들이 존재할 때 상태를 import하여 로드하는 컴포넌트
     * 로딩 시에 불러와 화면에 보여주기위한 컴포넌트이다.
     */
    // User,

    /**
     * AsyncUser Components
     * 비동기적으로 import되는 컴포넌트
     * 코드 스플리팅 기법으로 로드되는 컴포넌트이며, 해당 라우트를 방문했을때만 호출되어 모듈을 로딩하는 기법이다.
     *
     */
    AsyncUser,
  },
};
</script>

<style>
</style>