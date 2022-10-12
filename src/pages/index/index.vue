<template>
  <view>
    <!--    自定义导航栏-->
    <nav-bar>
      <!--      未切换状态-->
      <template v-if="checkedCount===0">
        <view slot="left" class="font-md ml-3 font-weight-bold ">首页</view>
        <template slot="right">
          <view style="width: 60rpx;height: 60rpx;"
                class="flex align-center justify-center bg-light rounded-md  mr-2">
            <text class="iconfont icon-zengjia"></text>
          </view>
          <view style="width: 60rpx;height: 60rpx;" class="flex align-center justify-center bg-light rounded-md mr-3">
            <text class="iconfont icon-gengduo"></text>
          </view>
        </template>
      </template>
      <!--      切换选择状态-->
      <template v-else>
        <view @click="unCheckAll" slot="left" class="font-md ml-3  text-main">取消</view>
        <text class="font-sm font-weight-bold">已选中{{ checkedCount }}个</text>
        <view @click="checkAll" slot="right" class="font-md mr-3  text-main">全选</view>
      </template>
    </nav-bar>
    <!--    自定义搜索框-->
    <view class="px-3 py-2">
      <view class="position-relative">
        <view style="height: 70rpx;width: 70rpx"
              class="position-absolute  top-0 left-0 flex align-center justify-center">
          <text class="iconfont icon-sousuo text-light-muted "></text>
        </view>
        <input type="text" style="height: 70rpx;padding-left: 70rpx" class="bg-light font-sm rounded-md "
               placeholder="搜索网盘文件"></input>
      </view>
    </view>
    <!--    列表-->
    <h-list @select="select" v-for="(item,index) in list" :key="index" :index="index" :item="item"/>
    <!--    底部操作条-->
    <view v-if="checkedCount!==0">
      <view style="height:115rpx"></view>
      <view style="height: 115rpx;" class="fixed-bottom flex align-stretch bg-main text-white">
        <view
            @click="handleBottomEvent(item)"
            v-for="(item,index) in actions" :key="index"
            class="flex-1 flex flex-column align-center justify-center"
            hover-class="bg-main-hover"
            style="line-height: 1.5">
          <text class="iconfont" :class="item.icon"></text>
          <text class="font-sm">{{ item.name }}</text>
        </view>
      </view>
    </view>
    <!--    弹出框-->
    <uni-popup ref="dialog">
      <view style="width:600rpx;" class="bg-white rounded-md">
        <view style="height: 100rpx" class="flex align-center justify-center  font-weight-bold">标题</view>
        <view class="flex align-center justify-center p-3"></view>
        <view style="height: 100rpx" class="flex">
          <view hover-class="bg-hover-light"  class="flex-1 text-muted flex align-center justify-center">取消</view>
          <view hover-class="bg-hover-light" class="flex-1 text-main flex align-center justify-center">确定</view>
        </view>
      </view>
    </uni-popup>
  </view>
</template>

<script>
import NavBar from "@/components/common/nav-bar";
import HList from "@/components/common/H-list";
import uniPopup from "@/components/uni-popup/uni-popup";

export default {
  components: {HList, NavBar},
  data() {
    return {
      // 列表数据
      list: [
        {
          type: "dir",
          name: "我的笔记",
          create_time: "2019-12-15 08:00",
          checked: false
        },
        {
          type: "image",
          name: "风景.jpg",
          create_time: "2019-12-15 08:00",
          checked: false
        },
        {
          type: "video",
          name: "uniapp实战课程.mp4",
          create_time: "2019-12-15 08:00",
          checked: false
        },
        {
          type: "text",
          name: "记事本.txt",
          create_time: "2019-12-15 08:00",
          checked: false
        },
        {
          type: "none",
          name: "压缩包.rar",
          create_time: "2019-12-15 08:00",
          checked: false
        }
      ]
    }
  },
  computed: {
    //选中的列表
    checkList() {
      return this.list.filter(item => {
        return item.checked
      })
    },
    //选中的数量
    checkedCount() {
      return this.checkList.length
    },
    //操作菜单
    actions() {
      if (this.checkedCount > 1) {
        return [
          {
            icon: 'icon-xiazai',
            name: '下载'
          },
          {
            icon: 'icon-shanchu',
            name: '删除'
          }
        ]
      } else {
        return [
          {
            icon: 'icon-xiazai',
            name: '下载'
          },
          {
            icon: 'icon-fenxiang-1',
            name: '分享'
          },
          {
            icon: 'icon-shanchu',
            name: '删除'
          },
          {
            icon: 'icon-chongmingming',
            name: '重命名'
          },
        ]
      }
    }
  }
  ,
  onLoad() {
  }
  ,
  methods: {
    //监听点击事件
    select(e) {
      this.list[e.index].checked = e.value
    }
    ,
    //全选事件
    checkAll() {
      this.list.map(item => {
        item.checked = true
      })
    }
    ,
    //取消全选
    unCheckAll() {
      this.list.map(item => {
        item.checked = false
      })
    },
    //处理底部操作条事件
    handleBottomEvent(item) {
      switch (item.name) {
        case '删除':
          this.$refs.dialog.open()
          break;
      }
    }
  }
}
</script>

<style>

</style>
