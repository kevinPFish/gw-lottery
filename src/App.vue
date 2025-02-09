<script setup lang="ts">
import PlayMusic from '@/components/PlayMusic/index.vue'
import useStore from '@/store'
import { themeChange } from '@/utils'
import { storeToRefs } from 'pinia'
import { onMounted } from 'vue'

const globalConfig = useStore().globalConfig
const prizeConfig = useStore().prizeConfig
const { getTheme: localTheme } = storeToRefs(globalConfig)
const { getPrizeConfig: prizeList } = storeToRefs(prizeConfig)


// 设置当前奖列表
function setCurrentPrize() {
  if (prizeList.value.length <= 0) {
    return
  }
  for (let i = 0; i < prizeList.value.length; i++) {
    if (!prizeList.value[i].isUsed) {
      prizeConfig.setCurrentPrize(prizeList.value[i])

      break
    }
  }
}
onMounted(() => {
  themeChange(localTheme.value.name)
  setCurrentPrize()
})
</script>

<template>
  <router-view />
  <PlayMusic class="absolute right-0 bottom-1/2" />
</template>

<style scoped lang="scss"></style>
