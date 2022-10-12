<template>
  <!--    自定义导航栏-->
  <view>
    <view class="fixed-top bg-white">
      <uni-status-bar> </uni-status-bar>
        <view style="height: 44px" class="flex align-center">
          <view class="flex-1 flex">
            <slot name="left"/>
          </view>
          <view class="flex-1 flex justify-center">
            <slot/>
          </view>
          <view class="flex-1 flex justify-end">
            <slot name="right"/>

          </view>
        </view>
    </view>
    <view>
      <uni-status-bar></uni-status-bar>
      <view style="height: 44px"></view>
    </view>
  </view>
</template>

<script>
import UniStatusBar from "@/components/uni-ui/uni-status-bar";

export default {
  name: "nav-bar",
  components: {UniStatusBar}
}
</script>

<style scoped>

</style>