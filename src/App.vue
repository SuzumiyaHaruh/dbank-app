<script>
export default {
  onLaunch: function () {
    console.log('App Launch')
  },
  onShow: function () {
    console.log('App Show')
  },
  onHide: function () {
    console.log('App Hide')
  }
}
</script>

<style>
/*每个页面公共css */
/*官方样式库*/
@import url("../src/common/uni.css");
/*公共样式*/
@import url("../src/common/common.css");
/*//引入自定义样式库*/
@import url("../src/common/free.css");
/*引入图标*/
@import url("../src/common/icon.css");

body {
  font-family: DIN-Medium, serif;
  color: #313131;
}
</style>
