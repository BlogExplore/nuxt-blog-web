<template>
  <nuxt-link :to="`/articleDetail/${item.id}`">
    <el-card shadow="hover" class="card-container">
      <div class="article-item">
        <div class="item-info">
          <div class="info-text">
            <h3>{{ item.title }}</h3>
            <div class="text-desc">
              {{ item.summary || '' }}
            </div>
            <!-- <div class="text-tag">
              标签：
              <VastTagsBox />
            </div> -->
          </div>
          <div class="info-data">
            <div class="data-view">
              <i class="el-icon-view"></i>
              <span>972</span>
            </div>
            <div class="data-view">
              <i class="el-icon-chat-round"></i>
              <span>12</span>
            </div>
            <div class="data-view">
              <i class="el-icon-price-tag"></i>
              <span>{{ item.labelCount || 9 }}</span>
            </div>
            <div class="data-view">
              <span>创建时间</span>
              <span> {{ item.createAt }} </span>
            </div>
            <div class="data-view">
              <span>作者：</span>
              <span> {{ item.author.username }} </span>
            </div>
          </div>
        </div>
        <div class="item-right-img">
          <img :src="item.coverImg" alt="" />
        </div>
      </div>
    </el-card>
  </nuxt-link>
</template>

<script lang="ts">
import { defineComponent } from '@nuxtjs/composition-api'

export default defineComponent({
  props: {
    item: {
      type: Object,
      default() {
        return {}
      },
    },
  },
  setup() {
    return {}
  },
})
</script>

<style lang="scss">
.card-container {
  .el-card__body {
    padding: 0;
    .article-item {
      padding: 20px;
      background-color: #fff;
      border: 1px solid #f0f0f0;
      overflow: hidden;
      display: flex;
      align-items: center;
      justify-content: space-between;
      cursor: pointer;
      .item-info {
        min-height: 120px;
        padding-right: 40px;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        .info-text {
          h3 {
            color: #333;
            margin-bottom: 20px;
            font-weight: 600;
            font-size: 20px;
            overflow: hidden;
            text-overflow: ellipsis;
            display: -webkit-box;
            -webkit-line-clamp: 2;
            -webkit-box-orient: vertical;
          }
          .text-tag {
            color: #666;
            margin: 10px 0;
            display: flex;
            align-items: center;
          }

          .text-desc {
            color: #666;
            overflow: hidden;
            text-overflow: ellipsis;
            display: -webkit-box;
            -webkit-line-clamp: 2;
            -webkit-box-orient: vertical;
            line-height: 1.3;
          }
        }
        .info-data {
          display: flex;
          align-items: center;
          color: #b4b4b4;
          .data-view {
            margin-right: 20px;
          }
        }
      }
      .item-right-img {
        width: 100px;
        height: 100px;
        img {
          width: 100px;
          height: 100px;
        }
      }
    }
  }
}
</style>
