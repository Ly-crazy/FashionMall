<template>
  <div class="swapper" ref="swapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
  import BetterScroll from 'better-scroll'
  import ObserveDOM from '@better-scroll/observe-dom'

  // BetterScroll.use(ObserveDOM)

  export default {
    name: 'Scroll',
    data() {
      return {
        scroll: null
      }
    },
    props: {
      probeType: {
        type: Number,
        default: 0
      },
      pullUpLoad: {
        type: Boolean,
        default: false
      }
    },
    methods: {
      // 相对于当前位置偏移滚动 x,y 的距离
      scrollTo(x, y, time) {
        this.scroll && this.scroll.scrollTo(x, y, time)
      },
      // 结束上拉加载行为
      finishPullUp() {
        this.scroll && this.scroll.finishPullUp()
      },
      // 重新计算 BetterScroll，当 DOM 结构发生变化的时候务必要调用确保滚动的效果正常
      refresh() {
        this.scroll && this.scroll.refresh()
      },
      // 获取 scroll 的 y 的距离
      getScrollY() {
        return this.scroll ? this.scroll.y : 0
      }
    },
    mounted() {
      // 创建 BetterScroll 对象
      this.scroll = new BetterScroll(this.$refs.swapper, {
        observeDOM: true,
        click: true,
        probeType: this.probeType,
        pullUpLoad: this.pullUpLoad
      })
      // 监听滚动位置
      if (this.probeType === 2 || this.probeType === 3) {
        this.scroll.on('scroll', (position) => {
          this.$emit('scroll', position)
        })
      }
      // 监听上拉事件(scroll滚动到底部)
      if (this.pullUpLoad) {
        this.scroll.on('pullingUp', () => {
          this.$emit('pullingUp')
        })
      }
    }
  }
</script>

<style scoped>

</style>