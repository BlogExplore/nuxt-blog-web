<template>
  <div>
    <header>
      <div class="follow-header follow-header-info">
        <div class="breadcrumb">
          <p class="cur">我的BiliBili粉丝（{{ total }}位）</p>
        </div>
      </div>
    </header>
    <VastFollowBiLi v-for="item in fetchedFans" :key="item.mid" :item="item" />
    <div class="page">
      <el-pagination
        background
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page="currentPage"
        :page-size="50"
        layout="total,prev, pager, next, jumper "
        :total="total"
      >
      </el-pagination>
    </div>
  </div>
</template>
<script lang="ts">
import {
  defineComponent,
  useFetch,
  ref,
  useStore,
  computed,
} from '@nuxtjs/composition-api'
interface IFanItem {
  mid: number
  uname: String
  face: string
  sign: string
}

export default defineComponent({
  setup(_props, context) {
    const fetchedFans = ref<IFanItem[]>([])
    const currentPage = ref(1)
    const total = ref(0)
    const handleSizeChange = () => {}
    const handleCurrentChange = (val: number) => {
      if (val > 5) {
        return
      }
      currentPage.value = val
      doFetch()
    }
    const { fetch: doFetch, fetchState } = useFetch(() => {
      return fetch(
        `http://localhost:2222/api/v1/bili/follows?vmid=310726273&pn=${currentPage.value}&ps=50`
      )
        .then((response) => response.json())
        .then((res) => {
          fetchedFans.value = res.data.list
          total.value = res.data.total
        })
    })
    doFetch()
    return {
      fetchedFans,
      handleSizeChange,
      handleCurrentChange,
      currentPage,
      total,
    }
  },
})
</script>

<style lang="scss" scoped>
.page {
  width: 100%;
  display: flex;
  justify-content: center;
  margin: 2rem 0;
}
.follow-header {
  border-bottom: 1px solid #e5e9ef;
  padding-bottom: 20px;
  min-height: 30px;
  margin: 20px 20px 0;
  .breadcrumb {
    line-height: 30px;
    font-size: 0;
    .cur {
      color: #222;
      font-size: 18px;
    }
  }
}
</style>
