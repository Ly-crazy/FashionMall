<template>
  <div class="goods">
    <goods-list-item v-for="item in goods" :goods-item="item" />
  </div>
</template>

<script>
  import GoodsListItem from './GoodsListItem'

  export default {
    name: 'GoodsList',
    components: {
      GoodsListItem
    },
    props: {
      goods: {
        type: Array,
        default() {
          return []
        }
      }
    }
  }
</script>

<style scoped>
  .goods {
    display: flex;
    /* 如果一条轴线排不下，换行，第一行在上方 */
    flex-wrap: wrap;
    /* 每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍 */
    justify-content: space-around;
    padding: 2px;
  }
</style>