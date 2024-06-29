<script setup>
import { ref } from 'vue';

const welcomeMessage = ref('欢迎来到我们的网站！');
const count = ref(0);
</script>

<template>
  <div class="welcome-container">
    <h1>{{ welcomeMessage }}</h1>
    <h2>您是第 {{ count }} 位访问者</h2>

    <div class="card">
      <button type="button" @click="count++">点击计数</button>
      <p>点击按钮查看访客计数。</p>
    </div>
  </div>
</template>

<style scoped>
.welcome-container {
  text-align: center;
  margin-top: 100px;
}

.card {
  margin: 0 auto;
  width: 50%;
  border: 1px solid #ccc;
  padding: 20px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}
</style>
