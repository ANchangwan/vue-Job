
<script setup>
import supabase from "../supabase.js";
import {onMounted, ref} from "vue";
import {useRouter} from "vue-router";


const router = useRouter();
const isLogin = ref(false); // 화면 표시 상태 변수

const name = ref('');
const addr = ref('사용자 주소');
const text = ref("IT와 웹 개발에 대한 열정을 가진 개발자입니다.")

onMounted(async () => {
  const { data: { user } } = await supabase.auth.getUser();

  if (user){
    console.log("로그인");
    isLogin.value = true;
    // user 정보 가져오기
    const { data, error } = await supabase
        .from('user_table')
        .select()
        .eq('id', user.id)
    if (data){
      name.value = data[0].name;
      addr.value = data[0].address;
      text.value = data[0].text;
    }else {
      console.log(data);
    }
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
    <div class="top-info-box">
      <img src="/vite.svg" alt="profile">
      <div class="right-info">
        <span class="name">{{ name }}</span>
        <address>{{ addr }}</address>
      </div>
    </div>
    <div class="text-info">
      <h4 class="text-info__title">자기소개</h4>
      <p class="text-info__introduce">{{ text }}</p>
    </div>
    <button @click="handleLogOut">로그아웃</button>

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
.top-info-box{
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 20px;
}
.text-info{
  display: flex;
  flex-direction: column;
  gap: 10px;
  .text-info__title{
    color: var(--main-color-dark);
    font-weight: bold;
    font-size: 18px;
  }
  .text-info__introduce{
    padding : 15px;
    border-radius: 5px;
    border : 1px solid var(--main-color-dark);
    width: 100%;
  }
}

</style>