<template>
  <div class="loading_info" v-if="loading">
    <span>회원가입 처리중</span>
  </div>
  <div class="form-container">
    <form @submit.prevent="handleSignup">
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
      <div class="form-group">
        <label for="tel">Phone</label>
        <input
            type="tel"
            id="tel"
            placeholder="010-1234-5678"
            required
            v-model="tel"
        />
      </div>
      <div class="form-group">
        <label for="name">Name</label>
        <input
            type="text"
            id="name"
            placeholder="이름 입력"
            required
            v-model="name"
        />
      </div>
      <div class="form-group">
        <label for="address">Address</label>
        <input
            type="text"
            id="address"
            placeholder="주소 입력"
            required
            v-model="address"
        />
      </div>
      <div class="form-group">
        <label for="text">자기소개</label>
        <textarea id="text" v-model="text"></textarea>
      </div>
      <button type="submit">회원가입</button>
    </form>
  </div>




</template>

<script setup>
import supabase from '../supabase';
import { ref } from 'vue';
import {useRouter} from "vue-router";

const email = ref('');
const password = ref('');
const tel = ref('');
const text = ref('');
const name = ref('');
const address = ref('');
const loading = ref(false);

const router = useRouter();

const handleSignup = async () => {
  loading.value = true;
  const { data, error } = await supabase.auth.signUp({
    email: email.value,
    password: password.value,
  })

  if(error) {
    alert(error.message)
  } else {
    console.log('회원가입 성공')
    const { error } = await supabase
        .from('user_table')
        .insert({
          id: data.user?.id,
          tel: tel.value,
          text: text.value,
          name: name.value,
          address: address.value,
        })
    if(error) {
      alert('에러')
      console.log(error)

    }else{
      alert("회원가입 성공");
      router.push('/');
    }
    loading.value = false;
  }

}

</script>

<style scoped>
@import url("../styles/form.scss");

</style>