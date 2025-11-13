<script lang="ts" setup>
import { useThemeStore } from '@/store'
import { safeAreaInsets } from '@/utils/systemInfo'

defineOptions({
  name: 'Home',
})
definePage({
  // 使用 type: "home" 属性设置首页，其他页面不需要设置，默认为page
  type: 'home',
  style: {
    // 'custom' 表示开启自定义导航栏，默认 'default'
    navigationStyle: 'custom',
    navigationBarTitleText: '首页',
  },
})

const themeStore = useThemeStore()

const description = ref(
  'unibest 是一个集成了多种工具和技术的 uniapp 开发模板，由 uniapp + Vue3 + Ts + Vite5 + UnoCss + VSCode 构建，模板具有代码提示、自动格式化、统一配置、代码片段等功能，并内置了许多常用的基本组件和基本功能，让你编写 uniapp 拥有 best 体验。',
)
console.log('index/index 首页打印了')

onLoad(() => {
  console.log('测试 uni API 自动引入: onLoad')
})

const searchType = ref<string>('全部')
const value = ref<string>('')
const menu = ref([
  {
    content: '全部'
  },
  {
    content: '订单号'
  },
  {
    content: '退款单号'
  }
])

function changeSearchType({ item, index }) {
  searchType.value = item.content
}

function search() {
  console.log('搜索')
}

const blocks = ref([
  {
    image: '../../static/images/1.png',
    name: '电动车租聘'
  }, {
    image: '../../static/images/1.png',
    name: '二手电动车'
  }, {
    image: '../../static/images/1.png',
    name: '配套商城'
  }, {
    image: '../../static/images/1.png',
    name: '找维修'
  }
])

const blocks2 = ref([
  {
    name: '123'
  }, {
    name: '123'
  }, {
    name: '123'
  }, {
    name: '123'
  }, {
    name: '123'
  }, {
    name: '123'
  }, {
    name: '123'
  }, {
    name: '123'
  }, {
    name: '123'
  }, {
    name: '123'
  }, {
    name: '123'
  }, {
    name: '123'
  },
])

const shows = ref([
  {
    name: '官方商城'
  }, {
    name: '官方商城'
  }, {
    name: '官方商城'
  },
])

// tabs
const tab = ref<number>(0)
const tabs = ref([
  {
    title: '推荐'
  }, {
    title: '附近'
  },
])

const listData = ref(
  {
    recommend: [
      {
        title: '便宜123',
        location: '常州市',
        endurance: '12-25',
        typeTag: ['商家车辆'],
        attrTag: ['同城车源'],
        price: 300,
        suggest_price: 400
      }, {
        title: '便宜123',
        location: '常州市',
        endurance: '12-25',
        typeTag: ['商家车辆'],
        attrTag: ['同城车源'],
        price: 300,
        suggest_price: 400
      }, {
        title: '便宜123',
        location: '常州市',
        endurance: '12-25',
        typeTag: ['商家车辆'],
        attrTag: ['同城车源', '质量三包'],
        price: 300,
        suggest_price: 400
      }
    ]
  }
)
</script>

<template>
  <view class="bg-black/5 px-4 pt-2" :style="{ marginTop: `${safeAreaInsets?.top}px` }">
    <wd-search v-model="value" hide-cancel @search="search">
      <template #prefix>
        <wd-popover mode="menu" :content="menu" @menuclick="changeSearchType">
          <view class="search-type">
            <text>{{ searchType }}</text>
            <wd-icon custom-class="icon-arrow" name="fill-arrow-down"></wd-icon>
          </view>
        </wd-popover>
      </template>
      <!-- <template #suffix>
        <wd-button>主要按钮</wd-button>
      </template> -->
    </wd-search>

    <!--  -->
    <view class="mt-2 p-2 bg-white rounded-t-xl">
      <view class="grid grid-cols-4 gap-4">
        <view v-for="item in blocks" :key="item.name"
          class="flex flex-col items-center gap-2 rounded-xl p-2 bg-blue-200">
          <image mode="aspectFill" :src="item.image" class="w-full h-12" />
          <view class="text-20rpx">{{ item.name }}</view>
        </view>
      </view>
    </view>

    <!-- grid -->
    <wd-grid :column="4" class="rounded-b-xl">
      <wd-grid-item icon="picture" :text="item.name" v-for="item in blocks2" :key="item.name" />
    </wd-grid>

    <!-- banner -->
    <image mode="aspectFill" src="../../static/images/2.png" class="mt-4 w-full h-22 rounded-xl" />

    <view class="text-gray-400 mt-4 flex items-center justify-between px-4 py-2 rounded-xl bg-white">
      <view v-for="item in shows" :key="item.name">
        <image src="../../static/images/1.png" class="size-6 mr-2" />
        <text class="text-22rpx">{{ item.name }}</text>
      </view>
    </view>

    <wd-tabs class="mt-4" v-model="tab">
      <block v-for="(item, index) in tabs" :key="item.title">
        <wd-tab :title="item.title">
          <view class="mt-4 flex flex-col gap-4">
            <view class="flex gap-4" v-for="data in listData.recommend" :key="data.title">
              <image class="h-full w-26 aspect-77/83 rounded-xl" src="../../static/images/avatar.jpg" />
              <view class="py-1 flex-1 flex flex-col gap-2">
                <view class="flex items-center">
                  <wd-tag custom-class="space" class="mr-2" type="primary" v-for="tTag in data.typeTag" :key="tTag">
                    {{tTag }}</wd-tag>
                  <text class="font-bold">{{ data.title }}</text>
                </view>

                <!-- Keep this block from expanding -->
                <view class="flex flex-col justify-end">
                  <view class="flex flex-col gap-1">
                    <view class="text-gray-400 flex items-center gap-2">
                      <span>续航{{ data.endurance }}公里</span>
                      <span>|</span>
                      <span>{{ data.location }}</span>
                    </view>
                  </view>

                  <!-- Tags section should not take remaining space -->
                  <view>
                    <wd-tag custom-class="space" class="mr-2" type="primary" v-for="aTag in data.attrTag" :key="aTag">
                      {{ aTag }}
                    </wd-tag>
                  </view>

                  <!-- Pricing section remains at the bottom -->
                  <view class="flex items-center gap-2">
                    <text class="font-800 text-red-600">售价 ￥{{ data.price.toFixed(2) }}</text>
                    <wd-tag plain class=" text-22rpx">官方指导价 ￥{{ data.price.toFixed(2) }}</wd-tag>
                  </view>
                </view>

              </view>

            </view>
          </view>
        </wd-tab>
      </block>
    </wd-tabs>
  </view>
</template>
<style lang="scss">
.search-type {
  position: relative;
  height: 30px;
  line-height: 30px;
  padding: 0 8px 0 16px;
}

.search-type::after {
  position: absolute;
  content: '';
  width: 1px;
  right: 0;
  top: 5px;
  bottom: 5px;
  background: rgba(0, 0, 0, 0.25);
}

.search-type {
  :deep(.icon-arrow) {
    display: inline-block;
    font-size: 20px;
    vertical-align: middle;
  }
}

// tabs
.content {
  line-height: 120px;
  text-align: center;
}
</style>