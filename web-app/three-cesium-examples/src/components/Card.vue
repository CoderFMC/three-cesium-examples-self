<template>
  <el-card class="card" shadow="hover" body-style="padding:15px">
    <div  v-if="data.image" class="preview-box" @click="openDemo">
      <transition name="el-zoom-in-center">
        <img
          :src="data.image"
          :alt="data.name"
          class="preview-image"
          @error="handleImageError"
        />
      </transition>
      <div class="image-overlay">
        <div class="hover-text">点击预览效果</div>
      </div>
    </div>
    <div  v-if="!data.image" class="no-img">
      <el-icon class="image-icon"><Picture /></el-icon>
      <span class="no-img-text">暂无封面</span>
    </div>

    <div class="content">
      <div class="title-row">
        <h3 class="title">{{ data.name }}</h3>
      </div>


      <p class="description">{{ data.des }}</p>

      <div class="actions">
        <el-button
          type="primary"
          @click="openDemo"
          :icon="ElIconLink"
          class="action-btn"
        >
          在线演示
        </el-button>
        <el-button
          type="success"
          @click="openSource"
          :icon="ElIconStar"
          class="action-btn"
        >
          查看源码
        </el-button>
      </div>
    </div>
  </el-card>
</template>

<script setup lang="ts">
import { ElIcon } from 'element-plus'
import { Link as ElIconLink, Star as ElIconStar } from '@element-plus/icons-vue'

const props = defineProps({
  data: {
    type: Object,
    required: true
  }
})

const handleImageError = (e) => {

}

const openDemo = () => {
  window.open(props.data.openUrl, '_blank')
}

const openSource = () => {
  window.open(props.data.githubUrl, '_blank')
}
</script>

<style scoped lang="less">
.card {
  width: 100%;
  height: 100%;
  transition: transform 0.3s, box-shadow 0.3s;
  border-radius: 8px;

  &:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 20px rgba(0,0,0,0.15);
  }

  .preview-box {
    position: relative;
    height: 200px;
    border-radius: 6px;
    overflow: hidden;
    cursor: pointer;
    transition: all 0.3s;

    &:hover {
      .image-overlay {
        opacity: 1;
      }

      .preview-image {
        transform: scale(1.05);
      }
    }

    .preview-image {
      width: 100%;
      height: 100%;
      object-fit: cover;
      transition: transform 0.3s;
    }

    .image-overlay {
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background: rgba(0,0,0,0.4);
      opacity: 0;
      transition: opacity 0.3s;
      display: flex;
      align-items: center;
      justify-content: center;

      .hover-text {
        color: white;
        font-size: 1.2rem;
        font-weight: 500;
        text-shadow: 1px 1px 3px rgba(0,0,0,0.5);
      }
    }
  }

  .content {
    padding: 15px 0;

    .title-row {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 12px;

      .title {
        margin: 0;
        font-size: 1.3rem;
        color: #333;
      }

      .author {
        font-size: 0.9rem;
        color: #666;
      }
    }

    .tip {
      color: #e6a23c;
      font-weight: 500;
      margin-bottom: 10px;
    }

    .description {
      font-size: 0.95rem;
      color: #666;
      line-height: 1.5;
      height: 60px;
      overflow: hidden;
      text-overflow: ellipsis;
      display: -webkit-box;
      -webkit-line-clamp: 3;
      -webkit-box-orient: vertical;
    }

    .actions {
      margin-top: 15px;
      display: flex;
      gap: 10px;

      .action-btn {
        flex: 1;
        transition: transform 0.2s;

        &:hover {
          transform: translateY(-2px);
        }
      }
    }
  }
  .no-img {
    position: relative;
    height: 200px;
    background: #f5f7fa;
    border-radius: 6px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: all 0.3s;

    &:hover {
      background: #e4e7ed;

      .image-icon {
        transform: scale(1.1);
      }

      .no-img-text {
        color: #409eff;
      }
    }

    .image-icon {
      font-size: 3rem;
      color: #c0c4cc;
      margin-bottom: 10px;
      transition: all 0.3s;
    }

    .no-img-text {
      color: #909399;
      font-size: 1.1rem;
      transition: color 0.3s;
    }
  }

  // 为保持布局一致，可以调整描述部分高度
  .description {
    height: 70px; // 从60px调整为70px
  }
}
</style>
