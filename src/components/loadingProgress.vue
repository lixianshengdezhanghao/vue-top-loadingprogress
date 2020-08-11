<template>
  <div class="loadingProgress">
    <div class="pace pace-inactive">
      <div class="pace-progress" :style="style"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'loadingProgress',

  props: {
    options: {
      type: Object,
      default() {
        return {
          succColor: '#264A9C',
          failColor: 'rgb(218, 26, 101)',
          position: 'top',
          transition: {
            widthSpeed: 200,
            opacitySpeed: 400,
            duration: 300, // 定义消失时间 ms
          },
          inverse: true, // 进度条的加载方向
          thickness: 2, // 进度条的高度
        };
      },
    },
  },

  data() {
    return {
      percent: 0, // 进度条长度
      show: false, // 显示和隐藏
      canSuccess: true, // 是否是成功的状态
    };
  },

  computed: {
    style() {
      // 先拿到乱七八糟的属性
      const { succColor, failColor, position, transition, inverse, thickness } = this.options;
      const { widthSpeed, opacitySpeed } = transition;
      const { canSuccess, percent, show } = this;

      // 定义 css 样式
      const style = {
        backgroundColor: canSuccess ? succColor : failColor,
        opacity: show ? 1 : 0,
      };

      if (position !== 'top' && position !== 'bottom') { // 传递属性出错时报错！！！
        throw new Error('The wrong config of position!'); 
      }

      style[position] = 0; // 创建style.top:0或者style.bottom:0

      if (inverse) {
        style.left = 0;
      } else {
        style.right = 0;
      }

      style.width = percent + '%'; // 设置进度条长度
      style.height = thickness + 'px'; // 设置显示高度
      style.transition = `width ${widthSpeed}ms, opacity ${opacitySpeed}ms`; // 设置过渡样式

      return style;
    },
  },
};
</script>

<style lang="scss" scoped>
.loadingProgress {
  // display: none;
  .pace .pace-progress {
    position: fixed;
    z-index: 100000;
    opacity: 1;
  }
}
</style>