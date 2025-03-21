<script setup lang="ts">
import { ref, onMounted } from 'vue'

const users = ref([])
const loading = ref(false)

const fetchUsers = async () => {
  loading.value = true
  try {
    const response = await fetch('http://localhost:3000/api/users')
    const data = await response.json()
    users.value = data
  } catch (error) {
    console.error('Error:', error)
  } finally {
    loading.value = false
  }
}

onMounted(() => {
  fetchUsers()
})
</script>

<template>
  <div class="user-page">
    <h1>用户列表,陈花是大美女</h1>
    <div v-if="loading">加载中...</div>
    <div v-else>
      <div v-for="user in users" :key="user.id" class="user-item">
        {{ user.name }}
      </div>
    </div>
  </div>
</template>

<style scoped>
.user-page {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

.user-item {
  padding: 10px;
  border-bottom: 1px solid #eee;
}
</style>