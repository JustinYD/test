<template>
  <div class="about">
  <van-cell>
  <van-col span="21">
    <span>蓝牙开关</span>
  </van-col>
    <van-switch v-model="flag" size="small"></van-switch>
  </van-cell>
  <van-cell v-show="flag">
      <van-picker
        title="蓝牙设备"
        show-toolbar
        :columns="columns"
        @confirm="onConfirm"
        @cancel="onCancel"
      />
    </van-cell>
    <van-cell style="margin-bottom:10px">
      <p>温度上限设置</p>
      <van-slider v-model="value" active-color="#0ac0ee">
        <template #button>
          <div class="custom-button">{{ value }}</div>
        </template>
      </van-slider>
    </van-cell>
    <van-cell>
      <p>湿度上限设置</p>
      <van-slider v-model="value1" active-color="#0ac0ee">
        <template #button>
          <div class="custom-button">{{ value1 }}</div>
        </template>
      </van-slider>
    </van-cell>
    
  </div>
</template>
<script>
import { Toast } from 'vant';
export default {
  data() {
    return {
      flag:true,
      value: 25,
      value1: 34,
      columns: ['iPhone11', '传感器', '小米8', '魅族16th'],
    };
  },
  methods: {
    onConfirm(value, index) {
      Toast(`正在连接：${value}, 当前索引：${index}`);
    },
    onCancel() {
      Toast('取消');
    },
  },
};
</script>
<style scoped>
.custom-button {
  width: 26px;
  color: #fff;
  font-size: 10px;
  line-height: 18px;
  text-align: center;
  background-color: #0ac0ee;
  border-radius: 100px;
}
</style>
