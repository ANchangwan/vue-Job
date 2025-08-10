<script setup>
import {ref} from "vue";

const title = ref('');
const todo = ref('');
const pay_rule = ref('');
const pay = ref("");


</script>

<template>
  <div class="form-container">
    <div class="form-group">
      <label for="title">제목</label>
      <input
          type="text"
          id="title"
          required
          placeholder="공고 내용을 요약해 주세요."
          v-model="title"
      />
    </div>
    <div class="form-group">
      <label for="todo">하는 일</label>
      <input
        type="text"
        id="todo"
        v-model="todo"
        placeholder="해야할 업무를 입력해주세요.s"
      />
    </div>
<!--    급여조건-->
    <div class="form-group">
      <input
          type="radio"
          id="pay_rule1"
          v-model="pay_rule"
          value="시급"
          name="pay_rule"
          required
          checked
      />
      <input
          type="radio"
          id="pay_rule2"
          v-model="pay_rule"
          value="월급"
          name="pay_rule"
          required
          checked
      />
      <div class="tab-group">
        <label for="pay_rule1">시급</label>
        <label for="pay_rule2">월급</label>
      </div>
    </div>
    <input
        type="number"
        id="pay"
        v-model="pay"
        required
        placeholder="시급 또는 월급을 입력해주세요!"
    />
  </div>
</template>

<style lang="scss" scoped>
@import url("../styles/form.scss");

.form-container {
  margin-top: 20px;
  padding-bottom: 50px;

  .tab-group {
    display: flex;
    gap: 15px;
    label {
      flex: 1;
      border: 1px solid var(--main-color-dark);
      border-radius: 8px;
      text-align: center;
      padding: 12px;
    }
  }

  input[type="radio"] {
    display: none;
  }

  input[type="radio"]:nth-child(1):checked ~ .tab-group label:nth-child(1) {
    background: var(--main-color-dark);
    color: #fff;
  }

  input[type="radio"]:nth-child(2):checked ~ .tab-group label:nth-child(2) {
    background: var(--main-color-dark);
    color: #fff;
  }

  #pay { margin-top: 8px;}

  // for=photo를 가진 form-group의 후손 input의 보더 스타일 제거
  .form-group:has(label[for=photo]) input {
    border: none;
  }

  //file 아이콘
  label[for=photo] {
    figure {
      display: flex;
      align-items: center;
      img {
        border: 1px solid red;
        margin-left: 30px;
      }
    }
  }
  input[type="file"] {
    display: none;
  }
}

.btn-submit {
  background: var(--main-color-light);
}

.form-group:has(label[for=photo]) {
  padding-bottom: 25px;
  border-bottom: 5px solid #ccc;
}
</style>