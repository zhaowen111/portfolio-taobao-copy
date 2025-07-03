<script setup>
import { computed } from 'vue';
import { ref } from 'vue';
/**
 * 1.一个始终显示的按钮，包含文字和1个可选的图标
 * 2.hover时文字变成橙色，可选是否弹出一个下拉选择框
 * 3.若需要弹出一个下拉选择框，则包含一个作为内容后缀的垂直方向箭头，默认向下，hover时动画旋转成向上
 * 4.hover状态下显示下拉选择框，鼠标离开选择器或下拉选择框区域则退出hover状态
 * 5.下拉选择框中的内容hover时显示灰色半透明背景
 * 6.下拉选项的内容超过一定数量时，显示滚动条。
 */

//  组件选项:{options:[{text:显示的文本值，link（可选），点击后跳转的链接}]}
const props = defineProps({
  options: {
    type: Array,
    required: true,
    validator: (v) => v.every(opt => 'text' in opt)
  },
  icon: String,

})

const hasMoreOptions = computed(() => props.options.length > 1);
const text = computed(() => props.options[0].text);

const iconImgStyle = { backgroundImage: `url("${props.icon})"` }
const active = ref(false);
const activeClass = computed(() => active.value ? 'active' : '')
function mouseenter() {
  clearTimeout(timeid);
  active.value = true;
}

let timeid = null;
function closeDropdown() {
  timeid = setTimeout(() => {
    active.value = false;
  }, 100)
}

function mouseleave() {
  closeDropdown();
}



function contentMouseEnter() {
  clearTimeout(timeid);
}

function contentMouseLeave() {
  closeDropdown();
}

</script>

<template>
  <div class="dropdown-select-container" >
    <div :class="['display-option', activeClass]" @mouseenter="mouseenter" @mouseleave="mouseleave">
      <span class="icon" v-if="props.icon" :style="iconImgStyle"></span>
      <a class="text">{{ text }}</a>
      <span v-if="hasMoreOptions">
        <span class="icon arrow"/>
      </span>
    </div>
    <div :class="['options-content-container', activeClass]" @mouseenter="contentMouseEnter" @mouseleave="contentMouseLeave">
      <div :class="['options-content',]" >
        <a class="option-item" v-for="opt in props.options.slice(1)" :href="opt.link">{{ opt.text }}
        </a>
      </div>
    </div>
  </div>
</template>


<style lang="scss" scoped>
.dropdown-select-container {
  position: relative;
  display: inline-block;



  .text {
    margin: 0 4px;
  }

  .display-option {
    display: flex;
    align-items: center;
    margin: 0 5px;
  }

  .display-option.active {
    .text {
      color: orange;
    }

    .arrow {
      transition: transform 0.4s cubic-bezier(0.68, -0.55, 0.27, 1.55);
      transform: rotate(180deg) translateZ(0);
    }
  }

  .icon {
    display: block;
    width: 15px;
    height: 15px;
    background-size: contain;
  }

  .arrow {
    width: 8px;
    height: 8px;
    background-image: url("src/assets/arrowunder.svg");


    /* 弹性效果 */
    transform-origin: center;
  }


  .options-content-container {
    position: absolute;
    margin-top: -1px;
    display: none;
    top: 100%;

    &.active {
      display: block;
    }

    .options-content {
      width: 100%;
      margin-top: 10px;
      border-radius: 12px;
      padding: 10px;
      box-shadow: 0px 4px 24px 0px rgba(10, 10, 51, 0.12),
        0px 0px 8px 0px rgba(0, 0, 0, 0.04);

      .option-item {
        display: block;
        box-sizing: border-box;
        padding: 5px 10px;
        border-radius: 5px;

        &:hover {
          background-color: rgba($color: #000000, $alpha: 0.1);
        }
      }
    }
  }
}
</style>