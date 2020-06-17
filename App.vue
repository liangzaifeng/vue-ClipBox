<template>
  <div id="app">
    <div class="header">header</div>
    <ClipBox
      :top="100"
      :wrapHeight="2000"
      :minCircleNum="10"
      :height="875"
      src="图片"
      v-model="circleNum"
    >
    </ClipBox>
    <div class="footer"></div>
  </div>
</template>

<script>
import ClipBox from '@/components/ClipBox';
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
