<template>
  <div class="doc-demo-picker">
    <div class="demo-title">Picker 单行</div>
    <div class="result" @click="showPicker">{{showText1}}</div>
    <div class="demo-box">
      <qiyi-picker :data="list1" :selected="selectedIndex1" ref="picker" @confirm="result" title="自定义title" hideTxt="关闭" confirmTxt="完成" optionKey="label"></qiyi-picker>
    </div>
  </div>
  
</template>

<script>
import Vue from "vue";
import qiyiPicker from "../src/index";
Vue.use(qiyiPicker);
export default {
  data() {
    return {
      list1: [{
        value: '1',
        label: '选项一'
      },
      {
        value: '2',
        label: '选项二'
      },
      {
        value: '3',
        label: '选项三'
      },
      {
        value: '4',
        label: '选项四'
      },
      {
        value: '5',
        label: '选项五'
      },
      {
        value: '6',
        label: '选项六'
      },
      {
        value: '7',
        label: '选项七'
      },
      {
        value: '8',
        label: '选项八'
      },
      {
        value: '9',
        label: '选项九'
      },
      {
        value: '10',
        label: '选项十'
      }],
      selectedIndex1: 0,
      showText1: "请选择",
    };
  },
  methods: {
    showPicker() {
      this.$refs.picker.show();
    },
    result(indexList) {
      this.selectedIndex1 = indexList;
      this.showText1 = this.list1[indexList].label;
    }
  }
}
</script>
<style lang="less">
.doc-demo-picker{
    position: relative;
    height: 647px;
    line-height: 2;
    color: #333;
    font-weight: 700;
    .demo-title{
        font-size: .12rem;
        padding: .05rem;
    }
    .demo-box {
        padding: .1rem;
        &.banner{
            padding-left: 0;
            padding-right: 0;
        }
    }
    .result{
        height: .5rem;
        width:100%;
        text-align: center;
        font-size:.16rem;
        line-height: .5rem;
        border-top:1px solid #999;
        border-bottom:1px solid #999;
        cursor: pointer;
    }
}
</style>

