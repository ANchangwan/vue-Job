<script setup>
import supabase from "../supabase.js";
import {onMounted, ref} from "vue";
import {useRouter} from "vue-router";


const router = useRouter();
const isLogin = ref(false); // 화면 표시 상태 변수

onMounted(async () => {
  const { data: { user } } = await supabase.auth.getUser();
  console.log(user.email);

  if (user){
    console.log("로그인");
    isLogin.value = true;
  }else {
    alert("로그인 후 사용해주세요!");
    isLogin.value = false;
    await router.push('/login');
  }
})
const handleLogOut = async () => {
  const { error } = await supabase.auth.signOut();
  if(error) {
    alert("로그아웃 실패");
  }
  await router.push('/');
}


</script>

<template>
  <div class="container" v-if="isLogin">
    <div class="form-container">
      <button @click="handleLogOut">로그아웃</button>
    </div>
  </div>

</template>

<style scoped>
button{
  background: transparent;
  color: var(--main-color-dark);
  font-size: 16px;
  margin-top: 40px;
  border: none;
  &:hover{
    opacity: 0.7;
    text-decoration: underline;
  }
}
</style>