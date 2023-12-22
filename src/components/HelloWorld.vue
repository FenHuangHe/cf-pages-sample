<script setup>

// 引入 fetch API
import {onMounted, ref} from "vue"

defineProps({
  msg: {
    type: String,
    required: true
  }
})


// 定义一个响应式的数据属性，用于存储从 worker 返回的数据
const message = ref("");

// 定义一个异步函数，用于发送请求并处理响应
const fetchMessage = async () => {
  // 使用 fetch 方法，向 worker 发送 GET 请求
  const response = await fetch("https://my-first-worker.richardhughes.workers.dev/");
  // 如果请求成功，使用 text() 方法将响应转换为文本
  const data = await response.text();
  // 将返回的数据赋值给 message 属性
  message.value = data;
};

// 在组件挂载后，调用 fetchMessage 函数
onMounted(fetchMessage);
</script>

<template>
  <div class="greetings">
    <h1 class="green">{{ message }}</h1>
    <h3>
      You’ve successfully created a project with
      <a href="https://vitejs.dev/" target="_blank" rel="noopener">Vite</a> +
      <a href="https://vuejs.org/" target="_blank" rel="noopener">Vue 3</a>.
    </h3>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
