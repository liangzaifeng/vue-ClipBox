今天看到小米手环5发布会, 滚动到一半时看到一个图片从圆变成占满一个屏幕,感觉挺有意思的, 就开发了这个组件

## Attributes
| 参数    | 说明               | 类型            | 可选择 | 默认值 |
| ------- | ------------------ | --------------- | ------ | ------ |
| v-model | 圆的大小 | Number | —     | 10     |
| minCircleNum | 圆大小的最小值 | Number | —     | 10     |
| top | 距离顶部的距离, 粘性布局使用的(不需要则不用传) | Number | —     | 0     |
| wrapHeight | 图片外层盒子的高度 | Number | —     | 0     |
| height | 图片的高度, 建议一个屏幕的高度, 效果好些(需要自己计算好传递进来) | Number | —     | 0     |
| src | 图片的路径 | String | —     | 空     |



```
<template>
  <div id="app">
    <div class="header">header</div>
    <ClipBox
      :top="100"
      :wrapHeight="2000"
      :minCircleNum="10"
      :height="875"
      src="图片路径"
      v-model="circleNum"
    >
    </ClipBox>
    <div class="footer"></div>
  </div>
</template>

<script>
import ClipBox from './components/ClipBox';
export default {
  name: 'app',
  components: { ClipBox },
  data() {
    return {
      circleNum: 10,
      mainHeight: 2000
    };
  }
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
.header {
  background-color: pink;
  height: 100px;
  width: 100%;
  position: fixed;
  top: 0;
  z-index: 10;
}

.footer {
  height: 2000px;
  background-color: yellowgreen;
}
</style>

