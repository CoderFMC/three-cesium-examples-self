

<template>
  <div class="aside">
    <el-row class="tac">
      <el-col :span="24">
        <el-menu
          active-text-color="#20c57d"
          background-color="#545c64"
          class="el-menu-vertical-demo"
          default-active="home"
          text-color="#fff"
          @select="handleOpen"
        >
          <el-menu-item index="home">
            <el-icon><icon-menu /></el-icon>
            <span>首页</span>
          </el-menu-item>
          <el-menu-item index="applicationScene">
            <el-icon><setting /></el-icon>
            <span>应用场景</span>
          </el-menu-item>
<!--          <el-menu-item index="shader">-->
<!--            <el-icon><setting /></el-icon>-->
<!--            <span>着色器</span>-->
<!--          </el-menu-item>-->
        </el-menu>
      </el-col>
    </el-row>
  </div>
</template>

<script setup lang="ts">
import {
  Document,
  Menu as IconMenu,
  Location,
  Setting,
} from '@element-plus/icons-vue'

const emit = defineEmits(['itemClick'])
const handleOpen = (key: string, keyPath: string[]) => {
  emit('itemClick',key)
}
const handleClose = (key: string, keyPath: string[]) => {
  console.log(key, keyPath)
}

</script>
<style scoped lang="less">
  .aside{
    height: 100%;
    width: 100%;
    border-top: 1px solid #999;
    background-color: #545c64;
  }
</style>
