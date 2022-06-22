<script setup lang="ts">
import { zhCN, zhTW, dateZhCN, dateZhTW, darkTheme, lightTheme } from 'naive-ui'
import { Sunny, Moon } from '@vicons/ionicons5'
type LocaleType = 'zhCN' | 'zhTW'
const locale = ref<LocaleType>('zhCN')
const isDark = ref(false)
const langOpt = [
  { label: '简体中文', key: 'zhCN' },
  { label: '繁体中文', key: 'zhTW' },
]
const langList = {
  zhCN: { locale: zhCN, label: '简体中文', dataLocale: dateZhCN },
  zhTW: { locale: zhTW, label: '繁体中文', dataLocale: dateZhTW },
}
const handleSelect = (e: LocaleType) => {
  locale.value = e
}
</script>
<template>
  <NConfigProvider
    :locale="langList[locale].locale"
    :date-locale="langList[locale].dataLocale"
    :theme="isDark === true ? darkTheme : lightTheme"
  >
    <NGlobalStyle />
    <div style="padding: 24px">
      <NSpace vertical>
        <NSpace>
          <NSwitch v-model:value="isDark" size="large">
            <template #checked-icon>
              <NIcon :component="Moon" color="#ffb900" />
            </template>
            <template #unchecked-icon>
              <NIcon :component="Sunny" color="#7f7f00" />
            </template>
          </NSwitch>
          <NDropdown trigger="hover" :options="langOpt" @select="handleSelect">
            <NButton>切换语言</NButton>
          </NDropdown>
        </NSpace>
        <NCard title="常用"
          ><NSpace vertical>
            <NSpace>
              <NButton>Default</NButton>
              <NButton type="tertiary"> Tertiary </NButton>
              <NButton type="primary"> Primary </NButton>
              <NButton type="info"> Info </NButton>
              <NButton type="success"> Success </NButton>
              <NButton type="warning"> Warning </NButton>
              <NButton type="error"> Error </NButton>
            </NSpace>
            <NSpace>
              <NTag> 爱在西元前 </NTag>
              <NTag type="success"> 不该 </NTag>
              <NTag type="warning"> 超人不会飞 </NTag>
              <NTag type="error"> 手写的从前 </NTag>
              <NTag type="info"> 哪里都是你 </NTag>
            </NSpace>
          </NSpace>
        </NCard>
        <NCard title="表单"
          ><NSpace vertical>
            <NSelect /><NInput /> <NTimePicker
          /></NSpace> </NCard
      ></NSpace>
    </div>
  </NConfigProvider>
</template>
<style></style>
