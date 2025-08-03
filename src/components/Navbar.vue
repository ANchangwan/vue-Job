<script setup>
import { Icon } from '@iconify/vue';
import { useRouter, useRoute } from "vue-router";
import {ref, watch} from "vue";

const router = useRouter(); // 경로 이동 시 사용
const route = useRoute();   // 현재 경로 정보

let currentPath = route.path;
let title = ref('')
watch(route, (newRoute) => {
  currentPath = newRoute.path;
  console.log(currentPath);

  if(currentPath === '/') {
    title.value = '로그인';
  }else if(currentPath === '/signup') {
    title.value = '회원가입';
  }else if(currentPath === '/job-detail') {
    title.value = 'job-detail'
  }else if(currentPath === '/job-post') {
    title.value = 'job-post'
  }else if(currentPath === '/job-list') {
    title.value = 'job-list'
  }else if(currentPath === '/job-profile') {
    title.value = 'job-profile'
  }
});
</script>

<template>
  <nav>
    <h1>{{ title }}</h1>
    <router-link
        v-if="currentPath === '/'
          || currentPath === '/signup'
          || currentPath === '/job-post'"
        to="/job-list"
        class="btn-close"
    >
      <Icon
          icon="material-symbols:close"
          width="24"
          style="color: #1e1e1e;"
      />
    </router-link>

    <!-- job-detail, user-profile 좌측 뒤로가기 아이콘 -->
    <router-link
        v-if="currentPath === '/job-detail' || currentPath === '/user-profile'"
        to="/job-list"
        class="btn-close"
    >
      <Icon
          icon="ic:baseline-arrow-back"
          width="24"
          height="24"
          style="color: 1e1e1e"
      />
    </router-link>

    <router-link
        v-if="currentPath === '/job-detail' || currentPath === '/user-profile'"
        to="/job-list"
        class="btn-close"
    >
      <Icon
          icon="ic:baseline-arrow-back"
          width="24"
          height="24"
          style="color: 1e1e1e"
      />
    </router-link>
    <!-- job-list 우측에 배치되는 프로필, 글쓰기 아이콘 -->
    <div class="right-icons" v-if="currentPath === '/job-list'">
      <router-link to="/user-profile">
        <Icon
            icon="teenyicons:user-circle-solid"
            width="24"
            style="color: #1e1e1e;"
        />
      </router-link>
      <router-link to="/job-post"><!-- post -->
        <Icon
            icon="mdi:pencil-outline"
            width="24"
            style="color: #1e1e1e;"
        />
      </router-link>
    </div>
  </nav>
</template>

<style lang="scss" scoped>
nav {
  position: relative;
  // background: pink;
  border-bottom: 1px solid #ccc;
  width: 100%;
  height: 44px;
  padding: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  h1 {
    font-size: 16px;
    color: var(--text-color-dark);
  }
  .btn-close {
    position: absolute;
    left: 15px;
    text-decoration: none;
  }
}

.right-icons {
  position: absolute;
  right: 15px;
  top: 10px;
  display: flex;
  gap: 10px;
}
</style>