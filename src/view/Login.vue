<template>
  <div class="loading_info" v-if="loading">
    <span>회원가입 처리중</span>
  </div>
  <div class="form-container">
    <form @submit.prevent="handleLogin">
      <div class="form-group">
        <label for="email">Email</label>
        <input
            type="email"
            id="email"
            placeholder="이메일 입력"
            required
            v-model="email"
        />
      </div>
      <div class="form-group">
        <label for="password">Password</label>
        <input
            type="password"
            id="password"
            placeholder="비밀번호 입력"
            required
            v-model="password"
        />
      </div>
      <button type="submit">로그인</button>
      <router-link to="/signup">회원가입</router-link>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRouter } from "vue-router";
import supabase from "../supabase";

const router = useRouter();
const isLoading = ref(false);

const email = ref('');
const password = ref('');

const handleLogin = async () => {
  isLoading.value = true;
  const { data, error } = await supabase.auth.signInWithPassword({
    email: email.value,
    password: password.value,
  });
  if(error) {
    alert(error.message);
    console.log(error);
  }else{
    alert("로그인 성공");
    await router.push('/job-list');
    isLoading.value = false;
  }
}

</script>

<style scoped>
@import url("../styles/form.scss");
@import url("../styles/loading.scss");
</style>