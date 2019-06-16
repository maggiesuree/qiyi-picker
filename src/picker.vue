<template>
  <div>
    <transition name="fade">
      <div class="mqu-picker-cover" v-show="display" @click="hide"></div>
    </transition>
    <div class="mqu-picker">
      <transition name="slide">
        <div class="picker" v-show="display">
          <div class="title">
            <span class="title-center">{{title}}</span>
            <a href="javascript:;" class="title-right" @click="confirm">{{confirmTxt}}</a>
          </div>
          <div class="picker-content">
            <div class="picker-up"></div>
            <div class="picker-down"></div>
            <div class="single">
              <div class="wheel" ref="wrapper">
                <ul class="list">
                  <li
                    v-for="item in dataList"
                    class="item"
                    :key="item[optionKey]"
                  >{{item[optionLabel]}}</li>
                </ul>
              </div>
            </div>
          </div>
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
import BScroll from "better-scroll";
export default {
  name: "qiyi-picker",
  data() {
    return {
      display: false,
      selectedIndex: this.selected,
      dataList: [],
      wheels: {}
    };
  },
  props: {
    data: {
      type: Array,
      default: []
    },
    selected: {
      type: Number,
      defalut: []
    },
    title: {
      type: String,
      default: "请选择"
    },
    confirmTxt: {
      type: String,
      default: "确定"
    },
    optionKey: {
      type: [String, Number],
      default: "value"
    },
    optionLabel: {
      type: String,
      default: "label"
    }
  },
  methods: {
    show() {
      this.display = true;
      this.__setData();
      this.$nextTick(() => {
        const wheelitem = this.$refs.wrapper;
        this.__createWheels(wheelitem);
      });
    },
    __createWheels(wheelitem) {
      this.wheels = new BScroll(wheelitem, {
        wheel: {
          selectedIndex: this.selectedIndex,
          rotate: 20,
          adjustTime: 10,
          wheel: "wheel-scroll",
          list: "wheel-item"
        },
        probeType: 3
      });
    },
    __setData() {
      this.dataList = [...this.data];
    },
    hide() {
      this.wheels.disable();
      this.dataList = [];
      this.display = false;
    },
    confirm() {
      this.wheels.stop();
      this.selectedIndex = this.wheels.getSelectedIndex();
      this.$emit("confirm", this.selectedIndex);
      this.hide();
    }
  }
};
</script>

<style lang="less">
.mqu-picker-cover {
  position: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background: rgba(0, 0, 0, 0.4);
}
.mqu-picker {
  position: fixed;
  bottom: 0;
  left: 0;
  border-top-left-radius: 0.1rem;
  border-top-right-radius: 0.1rem;
  width: 100%;
  background-color: #fff;
  z-index: 9999;
  overflow: hidden;
  .item {
    font-size: 0.14rem;
  }
  .slide-enter,
  .slide-leave-to {
    opacity: 0.5;
    transform: translate3d(0, 270px, 0);
  }

  .slide-enter-active,
  .slide-leave-active {
    transition: all 0.3s ease;
  }
  .title-center {
    display: block;
    height: 0.6rem;
    line-height: 0.6rem;
    text-align: center;
    font-size: 0.13rem;
  }
  .list {
    margin-top: 0.68rem;
    line-height: 0.36rem;
    padding-left: 0;
  }
  .title {
    border: 1px solid #e6e6e6;
  }
  .title a {
    display: block;
    top: 0;
    width: 0.4rem;
    height: 0.6rem;
    line-height: 0.6rem;
    position: absolute;
    font-size: 0.13rem;
    color: #34bc6e;
    text-decoration: none;
  }
  .title-left {
    text-align: left;
    left: 0.13rem;
  }
  .title-right {
    text-align: right;
    right: 0.13rem;
  }
  .single {
    display: flex;
    position: relative;
    height: 1.73rem;
    overflow: hidden;
  }
  .wheel {
    position: relative;
    flex: 1;
    height: 1.73rem;
    overflow: hidden;
  }
  .picker-content {
    position: relative;
    top: 0.2rem;
  }
  .picker-up {
    position: absolute;
    top: 0;
    z-index: 10;
    width: 100%;
    height: 0.68rem;
    background: -webkit-gradient(
      linear,
      left bottom,
      left top,
      from(hsla(0, 0%, 100%, 0.4)),
      to(hsla(0, 0%, 100%, 0.8))
    );
    background: linear-gradient(
      0deg,
      hsla(0, 0%, 100%, 0.4),
      hsla(0, 0%, 100%, 0.8)
    );
    border-bottom: 1px solid #e6e6e6;
    pointer-events: none;
  }
  .picker-down {
    position: absolute;
    bottom: 0;
    z-index: 10;
    width: 100%;
    height: 0.68rem;
    background: -webkit-gradient(
      to bottom,
      rgba(255, 255, 255, 0.4),
      rgba(255, 255, 255, 0.8)
    );
    background: linear-gradient(
      to bottom,
      rgba(255, 255, 255, 0.4),
      rgba(255, 255, 255, 0.8)
    );
    border-top: 1px solid #e6e6e6;
    pointer-events: none;
  }
  .item {
    display: block;
    width: 100%;
    text-align: center;
  }
  .picker {
    z-index: 9999;
  }
}
</style>
