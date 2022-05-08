<template>
  <div class="home">
    <carousel
        :navigation="true"
        :pagination="true"
        :start-auto-play="false"
        :timeout="100000"
        class="carousel"
        v-slot="{ currentSlide }">
      <!-- 循环-->
      <slide v-for="(slide,index) in carouselSlides" :key="index">
        <!--当 v-show_“条件”为 true 时显示元素-->
        <!-- <div v-show="checkflg">チェックが入るとこの要素が表示されます</div>-->
        <!--<div v-show="!checkflg">チェックが入っていませんので表示されません</div>-->
        <div v-show="currentSlide === index +1" class="slide-info">
          <!-- 使用${}进行拼接-->
          <img :src="require(`../assets/${slide}.jpg`)" alt=""/>
        </div>
      </slide>
    </carousel>

  </div>
</template>

<script>
import carousel from "@/components/Carousel";
import slide from "@/components/Slide";
export default {
  name: 'HomeView',
  components: {carousel,slide},
  setup(){
    //创建一个图片的数组
    const carouselSlides=["bg-1","bg-2","bg-3"];
    return{ carouselSlides };

  },
}
</script>

<style lang="scss" scoped>


.carousel{
  //vh：视口（屏幕大小）高度的百分比。 100vh 表示与屏幕高度相同 （100%）
  //vw：视口宽度的百分比
  max-height: 100vh;
  height: 100vh;
  overflow: hidden;


  .slide-info {
    display: flex;
    position: relative;
    align-items: center;
    justify-content: center;
    //left: 300px;
    //让所有图片全部置顶
    //width: 80%;
    //height: 800px;


    img{
      width: 530px;
      //object-fit 属性可接受如下值：
      //fill - 默认值。调整替换后的内容大小，以填充元素的内容框。如有必要，将拉伸或挤压物体以适应该对象。
      //contain - 缩放替换后的内容以保持其纵横比，同时将其放入元素的内容框。
      //cover - 调整替换内容的大小，以在填充元素的整个内容框时保持其长宽比。该对象将被裁剪以适应。
      object-fit: fill;
      //transform: translate(0,-60px);
    }
  }
}
</style>

