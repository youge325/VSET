<script lang="ts">
import { useRouter } from 'vue-router'
import { defineComponent, h, ref, Component } from 'vue'
import { NIcon } from 'naive-ui'
import type { MenuOption } from 'naive-ui'
import {
  BookOutline as homeIcon,
  AddCircleOutline as inputIcon,
  ConstructOutline as enhanceIcon,
  CameraOutline as filterIcon,
  ColorFillOutline as outputIcon,
  SendOutline as rendingIcon,
  SettingsOutline as settingIcon
} from '@vicons/ionicons5'

function renderIcon (icon: Component) {
  return () => h(NIcon, null, { default: () => h(icon) })
}

const menuOptions: MenuOption[] = [
  {
    whateverLabel: '主页',
    whateverKey: 'home',
    icon: renderIcon(homeIcon),
    path:'/'
  },

  {
    whateverLabel: '输入',
    whateverKey: 'input',
    icon: renderIcon(inputIcon)
    ,
    path:'/input'
  },

  {
    whateverLabel: '增强',
    whateverKey: 'enhance',
    icon: renderIcon(enhanceIcon),
    path:'/enhance'
  },

  {
    whateverLabel: '滤镜',
    whateverKey: 'filter',
    icon: renderIcon(filterIcon),
    path:'/filter'
  },

  {
    whateverLabel: '输出',
    whateverKey: 'output',
    icon: renderIcon(outputIcon),
    path:'/output'
  },

  {
    whateverLabel: '渲染',
    whateverKey: 'rending',
    icon: renderIcon(rendingIcon),
    path:'/rending'
  },
  {
    whateverLabel: '设置',
    whateverKey: 'setting',
    icon: renderIcon(settingIcon),
    path:'/setting'
  }

]


export default defineComponent({
  setup () {
    const router = useRouter()
    const onMenuChange = (value: string) => {
      router.push(value)
    }

    router.push('/home')

    return {
      collapsed: ref(true),
      menuOptions,
      onMenuChange
    }
  }
})
</script>

<template>
  <n-message-provider>
    <div class="app-container">
      <n-layout has-sider>
        <n-layout-sider
          class="custom-sider"
          bordered
          collapse-mode="width"
          :collapsed-width="64"
          :width="120"
          :collapsed="collapsed"
          show-trigger
          @collapse="collapsed = true"
          @expand="collapsed = false"
          
        >
          <n-menu
            :collapsed="collapsed"
            :collapsed-width="64"
            :collapsed-icon-size="22"
            :options="menuOptions"
            key-field="whateverKey"
            label-field="whateverLabel"
            children-field="whateverChildren"
            @update:value="onMenuChange"
  
          />
        </n-layout-sider>

        <n-layout-content content-style="padding: 24px;">
          <router-view></router-view>
        </n-layout-content>
      </n-layout>
    </div>
  </n-message-provider>
</template>


<style scoped>
.custom-sider {
  background-color: #D0EBFF !important;
}

.app-container {
  display: flex;
  height: 100vh;
}

.n-layout-sider {
  flex: 0 0 120px; /* 固定宽度 */
}

.router-view {
  flex: 1; /* 自动填充剩余空间 */
}

.router-view-container {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
}

</style>