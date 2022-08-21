<template>
  <div>Login</div>
</template>

<script lang="ts" setup>
import { getLoginInfo } from '@/api/common'
import { ILoginInfo } from '@/api/types/common'
import { onMounted, ref } from 'vue'

const list = ref < ILoginInfo['slide'] > ([])

onMounted(() => {
  getLoginInfo().then(res => {
    console.log(res.login_logo)
    list.value = res.slide
  })
})
</script>
<style lang="scss" scoped></style>
