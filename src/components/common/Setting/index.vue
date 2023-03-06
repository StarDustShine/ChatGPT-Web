<script setup lang='ts'>
import { computed, ref } from 'vue'
import { NCard, NModal, NTabPane, NTabs } from 'naive-ui'
import General from './General.vue'
import About from './About.vue'
import { SvgIcon } from '@/components/common'

const props = defineProps<Props>()

const emit = defineEmits<Emit>()

interface Props {
  visible: boolean
}

interface Emit {
  (e: 'update:visible', visible: boolean): void
}

const active = ref('General')

const reload = ref(false)

const show = computed({
  get() {
    return props.visible
  },
  set(visible: boolean) {
    emit('update:visible', visible)
  },
})

function handleReload() {
  reload.value = true
  setTimeout(() => {
    reload.value = false
  }, 0)
}
</script>

<template>
</template>
