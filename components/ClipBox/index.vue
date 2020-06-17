<template>
  <div
    class="clip-box-wrap"
    ref="clipBox"
    :style="{ height: wrapHeight + 'px' }"
  >
    <div
      class="sticky"
      :style="{
        'clip-path': 'circle( ' + circleNum + '%)',
        top: top ? top + 'px' : 0,
        background: 'url(' + src + ') no-repeat center center',
        height: height + 'px'
      }"
    ></div>
  </div>
</template>
<script>
export default {
  model: {
    prop: 'circleNum'
  },
  props: {
    // 距离顶部的距离, 粘性布局使用的
    top: {
      type: Number,
      default: 0
    },
    // 图片外层盒子的高度
    wrapHeight: {
      type: Number,
      default: 0
    },
    // 图片的高度, 建议一个屏幕的高度, 效果好些(需要自己计算好传递进来)
    height: {
      type: Number,
      default: 0
    },
    // 圆的大小
    circleNum: {
      type: Number,
      default: 10
    },
    // 最小圆的大小
    minCircleNum: {
      type: Number,
      default: 10
    },
    // 图片的路径
    src: {
      type: String,
      default: ''
    }
  },
  name: 'ClipBox',
  mounted() {
    window.addEventListener('scroll', this.countCircleNum);
  },
  beforeDestroy() {
    window.removeEventListener('scroll', this.countCircleNum);
  },
  methods: {
    countCircleNum() {
      console.log('我生效了');

      let clipBoxTop = this.$refs.clipBox.offsetTop;
      const currentScrollTop = document.documentElement.scrollTop;
      const { wrapHeight, top } = this;
      if (currentScrollTop - clipBoxTop > wrapHeight + top) return; // 超出了不计算

      const { circleNum, minCircleNum, height } = this;
      let countCircle = undefined;
      // 超过的顶部距离
      if (currentScrollTop > top) {
        // 计算数值
        let countHeight =
          ((currentScrollTop - clipBoxTop - top) / (wrapHeight - height)) * 100;

        countCircle =
          countHeight > 100
            ? 100
            : countHeight < minCircleNum
            ? minCircleNum
            : countHeight;
      } else {
        if (circleNum === minCircleNum) return;
        // 兜底预防计算不准
        countCircle = circleNum <= minCircleNum ? minCircleNum : circleNum;
      }

      if (countCircle !== circleNum) {
        // 不重复的才更新值
        this.$emit('input', countCircle);
      }
    }
  }
};
</script>
<style lang="scss" scoped>
.sticky {
  position: sticky;
  width: 100%;
}
.clip-box-wrap {
  width: 100%;
}
</style>
