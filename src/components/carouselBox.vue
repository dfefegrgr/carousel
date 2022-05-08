<template>
  <div class="carousel">
    <slot :currentSlide="currentSlide"/>
    <!--    导航-->
    <div v-if="navEnable" class="navigate">
      <!--      切换页面按钮-->
      <div class="toggle-page left">
        <div @click="prevSlide" class="lefticon"></div>
      </div>
      <div class="toggle-page right">
        <div @click="nextSlide" class="righticon"></div>
      </div>

    </div>
    <!--    pagination 分页-->
    <div v-if="paginationEnable" class="pagination">
      <!-- 判断当(index===标识)时添加active-class-->
      <span
          @click="goToSlide(index)"
          v-for="(slide,index) in getSlideCount"
            :key="index"
            :class="{active:index+1===currentSlide}"
      >

      </span>
    </div>

  </div>

</template>

<script>
import {ref,onMounted} from  "vue"
export default {
  props:["startAutoPlay","timeout","navigation","pagination"],
  setup(props){
    //当前图片
    const currentSlide = ref(1);
    const getSlideCount = ref(null)
    const autoPlayEnable = ref(props.startAutoPlay === undefined ? true : props.startAutoPlay)
    const timeoutDuration = ref(props.timeout === undefined ? true : props.timeout)
    const paginationEnable = ref(props.pagination === undefined ? true : props.pagination)
    const navEnable = ref(props.navigation === undefined ? true : props.navigation)
    //下一个
    //下一个

    const nextSlide=()=>{
      if (currentSlide.value===getSlideCount.value){
        currentSlide.value=1;
        return;
      }
      console.log(currentSlide.value)
      currentSlide.value+=1;

    }
    //上一个
    const prevSlide=()=>{
      if (currentSlide.value===1){
        currentSlide.value =1;
        return;
      }
      currentSlide.value-=1;
    }
    //翻页
    const goToSlide =(index)=>{
      currentSlide.value=index+1
    }

    //自动播放
    const autoPlay =()=>{
      setInterval(()=>{
        nextSlide()
      },timeoutDuration.value)
    }
    //执行自动播放
    if(autoPlayEnable.value){
      autoPlay()
    }
    //onMounted(钩子），第一次渲染时做什么
    onMounted(()=>{
      getSlideCount.value= document.querySelectorAll('.slide').length;
      console.log(getSlideCount.value)
    })
    return{currentSlide,prevSlide,nextSlide,getSlideCount,
      goToSlide,paginationEnable,navEnable};
  },

};

</script>

<style>
.navigate{
  padding: 0 16px;
  height: 100%;
  width: 100%;
  position: absolute;
  top: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}
.toggle-page{
  display: flex;
  /*flex:1 只拉伸指定的弹性项目*/
  flex: 1;
}
.right{
  justify-content: flex-end;
}
.righticon{
    width: 0;
    height: 0;
    border: 20px solid ;
    border-color:  transparent transparent transparent mediumaquamarine;
}
.lefticon{
    width: 0;
    height: 0;
    border: 20px solid;
    border-color:  transparent mediumaquamarine transparent transparent ;
}
.pagination{
  position: absolute;
  bottom: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  gap: 30px;}

 span {
  /*设置鼠标指针位于元素上时显示的鼠标光标类型。*/
  cursor: pointer;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background-color: aquamarine;
  box-shadow: 0 1px 3px 0 rgba(0,0,0,0.1),0 1px 2px 0 rgba(0,0,0,0.06);
}
.active {
  background-color: white;
}


</style>