<script setup lang='ts'>
import { onMounted, ref } from 'vue'
import { NSpin } from 'naive-ui'
import { fetchChatConfig } from '@/api'
import pkg from '@/../package.json'

interface ConfigState {
  timeoutMs?: number
  reverseProxy?: string
  apiModel?: string
  socksProxy?: string
}

const loading = ref(false)

const config = ref<ConfigState>()

async function fetchConfig() {
  try {
    loading.value = true
    const { data } = await fetchChatConfig<ConfigState>()
    config.value = data
  }
  finally {
    loading.value = false
  }
}

onMounted(() => {
  fetchConfig()
})
</script>

<template>
  <NSpin :show="loading">
    <div class="p-4 space-y-4">
      <h2 class="text-xl font-bold">
        恩科NTCOR - ChatGPT-3.5Turbo
      </h2>
      <div class="p-2 space-y-2 rounded-md bg-neutral-100 dark:bg-neutral-700">
        <p>
          问心我爱你问心我爱你问心我爱你问心我爱你问心我爱你问心我爱你问心我爱你问心我爱你问心我爱你问心我爱你问心我爱你问心我爱你问心我爱你
        </p>
      </div>
      <p>运行模式：{{ config?.apiModel ?? '-' }}</p>
      <p>许可域名：{{ config?.reverseProxy ?? '-' }}</p>
      <p>超时时间：{{ config?.timeoutMs ?? '-' }}</p>
      <p>代理情况：{{ config?.socksProxy ?? '未启用Socks5' }}</p>
    </div>
  </NSpin>
</template>
