<template>
  <!--  列表-->
  <view class="p-3  flex  align-center">
    <!--      文件图标-->
    <text class="iconfont" :class="iconClass" style="font-size: 60rpx;"></text>
    <!-- 文件信息-->
    <view class="flex flex-column ml-3" style="line-height: 1.2;">
      <text class="font">{{ item.name }}</text>
      <text class="font-sm text-muted">{{ item.create_time }}</text>
    </view>
    <view
        class="ml-auto flex justify-center align-center" style="width: 70rpx;height: 70rpx"
        @click.stop="select"
    >
      <!--        未选中-->
      <text v-if="!item.checked" style="width: 25rpx;height: 25rpx;" class="rounded-circle border"></text>
      <!--        选中-->
      <text v-else class="iconfont icon-xuanze-yixuan text-main"></text>
    </view>
  </view>
</template>

<script>
const icons = {
  // 图标属性
  dir: {
    value: 'icon-file-b-2',
    color: 'text-warning'
  },
  image: {
    value: 'icon-file-b-6',
    color: 'text-success'
  },
  video: {
    value: 'icon-file-b-9',
    color: 'text-primary'
  },
  text: {
    value: 'icon-file-b-7',
    color: 'text-info'
  },
  none: {
    value: 'icon-file-b-8',
    color: 'text-muted'
  }
}
export default {
  name: "H-list",
  props: {
    item: {
      type: Object,
      required: true
    },
    index: {
      type: [Number, String],
      required: true
    }
  },
  computed: {
    iconClass() {
      let item = icons[this.item.type]
      return `${item.value} ${item.color}`
    }
  },
  methods: {
    //选择事件
    select() {
      this.$emit('select', {
        index: this.index,
        value: !this.item.checked
      })
    }
  },
}
</script>

<style scoped>

</style>