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
      scrollTo(x, y, time) {
        this.scroll.scrollTo(x, y, time)
      },
      finishPullUp() {
        this.scroll.finishPullUp()
      }
    },
    mounted() {
      // 创建 BetterScroll 对象
      this.scroll = new BetterScroll(this.$refs.swapper, {
        observeDOM: true,
        click: true,
        // mouseWheel: true
        probeType: this.probeType,
        pullUpLoad: this.pullUpLoad
      })
      // 监听滚动位置
      this.scroll.on('scroll', (position) => {
        this.$emit('scroll', position)
      })
      // 监听上拉事件
      this.scroll.on('pullingUp', () => {
        this.$emit('pullingUp')
      })
    }
  }
</script>

<style scoped>
  
</style>