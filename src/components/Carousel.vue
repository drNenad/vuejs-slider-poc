<template>
  <div class="wrapper" >
    <transition :name="transition" >
      <div class="carousel" :key="this.slideArrayIndex" >
        <slot></slot>
      </div>
    </transition>
    <a class="carousel__nav carousel__prev" @click.prevent="prev" href="#"><i class="fa fa-chevron-circle-left" aria-hidden="true"></i></a>
    <a class="carousel__nav carousel__next" @click.prevent="next" href="#"><i class="fa fa-chevron-circle-right" aria-hidden="true"></i></a>
    <div class="carousel__pagination" v-if="numOfSlides<=1">
      <a v-for="n in paginationNumber" @click="goto(n-1)" :class="{active: n-1==index[0]}" :key="n"><i class="fa fa-circle" aria-hidden="true"></i></a>
    </div>
  </div>
</template>

<script>
  export default {
    props:['autoplaySpeed','numOfSlides','animationstyle'],
    data(){
      return{
          slideIndexFirse: Object,
          index : 0,
          slideIndex: 0,
          slideArrayIndex:0,
          paginationNumber:3,
          slides: [],
          autoplay: false,
          my_timer: 0,
          direction: ''
      }
    },
    created(){
      if(this.autoplay==true){
           this.my_timer = setInterval(this.next, this.autoplaySpeed)
           return true
      }
      else{
        return false
      }

    },
    watch: {
      slides(slides) {
        if(this.index >= this.slidesCount){
          this.index = 0
        }
      }
    },
    computed: {
        slidesCount(){
          this.slides = this.$children
          this.slides.forEach((slide,i) => {
            slide.index = i
          })
          return this.slides.length
        },
        transition(){
          if(this.animationstyle=="slide"){
            return 'slide'
          }
          else{
            if (this.direction){
              return 'animate-' + this.direction
            }
          }
          console.log(this.direction)
        }
    },

    mounted(){
      this.slides=this.$children
      if(this.numOfSlides>=0){
        this.index=[]
         for(var i=0; i < this.numOfSlides; i++){
            this.index.push(i)
         }
      }
       this.paginationNumber=Math.ceil(this.slidesCount/this.numOfSlides)
        console.log(this.paginationNumber)
    },
    methods: {
      clearAutoplay(){
        if(this.autoplay==true){
          clearInterval(this.my_timer)
          this.my_timer = setInterval(this.next,this.autoplaySpeed)
        }
        else{
          return false
        }
      },
      next(){
        this.direction = 'right'
        if(Array.isArray(this.index)){
          if(this.slideIndex>(this.slidesCount-1)-this.numOfSlides){
             this.slideIndex=0
           }
           else if(this.slideIndex<0){
             this.slideIndex=0+this.numOfSlides
           }
           else{
             this.slideIndex+=this.numOfSlides
           }
           this.slideArrayIndex = Math.min(this.slideIndex, this.slidesCount-this.numOfSlides)
           if(this.slideArrayIndex==this.slidesCount-this.numOfSlides){

           }
           for (var i=0; i<this.numOfSlides; i++){
             this.index.splice(i, 1, i+this.slideArrayIndex)
           }
        }

        else {
            this.index++
             if(this.index >= this.slidesCount){
             this.index = 0
          }
        }
        this.clearAutoplay()
      },
      scrollingMethod(index){
        for(var i=0; i<=this.index.length; i++){
          if(this.index[i]>this.slideIndex){
            return true
          }
          else{
            return false
          }
        }
      },
      prev(){
        this.direction = 'left'
        if(Array.isArray(this.index)){
            if(this.slideIndex <= 0) {
              this.slideIndex = this.slidesCount - this.numOfSlides
            }
            else if (this.slideIndex > this.slidesCount - this.numOfSlides) {
              this.slideIndex = (this.slidesCount - this.numOfSlides)-this.numOfSlides
            }
            else {
              this.slideIndex -= this.numOfSlides
            }
          this.slideArrayIndex = Math.max(0,this.slideIndex)
          for (var i=0; i<this.numOfSlides; i++){
            this.index.splice(i, 1, i+this.slideArrayIndex)
          }
        }
       else{
          this.index --
          if(this.index < 0) {
            this.index = this.slidesCount - 1
          }
       }
       this.clearAutoplay()
      },
      goto(index){
//        clearInterval(this.my_timer)
//        this.my_timer = setInterval(this.next,this.autoplaySpeed)
          this.index[0]=index
          this.slideArrayIndex=index
          this.slideIndex=index
          this.direction="right"

        console.log(index)
      }
    }
  }
</script>

<style scoped>
.wrapper{
  position: relative;
  overflow: hidden;
}
.carousel{
    display: -webkit-box;
    position: relative;
    width: 100%;
    height: 100%;
}
.carousel img{
  position: relative;
}
.carousel__nav{
    position: absolute;
    top: 50%;
    transform: translate(-50%,-50%);
    font-size: 50px;
    color: rgba(255, 255, 255, 0.3);
    z-index: 1000;
}
.carousel__nav:hover{
    color: rgba(255, 255, 255, 0.7);
    -webkit-transition: all 0.3s ease-in-out;
    -moz-transition: all 0.3s ease-in-out;
    -ms-transition: all 0.3s ease-in-out;
    -o-transition: all 0.3s ease-in-out;
    transition: all 0.3s ease-in-out;
}
.carousel__prev{
    left: 50px;
}
.carousel__next{
    right: 15px;
}
.carousel__pagination{
    position: absolute;
    bottom: 20px;
    left: 50%;
    transform: translate(-50%,-50%);
}
.carousel__pagination a{
    margin-right: 15px;
    color: rgba(255, 255, 255, 0.3);
}
.carousel__pagination a:hover{
    color: rgba(255, 255, 255, 0.7);
    -webkit-transition: all 0.3s ease-in-out;
    -moz-transition: all 0.3s ease-in-out;
    -ms-transition: all 0.3s ease-in-out;
    -o-transition: all 0.3s ease-in-out;
    transition: all 0.3s ease-in-out;
}
.carousel__pagination .active{
    color: #2196F3;
}
.carousel__pagination .active:hover{
    color: #2196F3;
}
.slide-enter-active{
    animation: slideIn 1s;
}
.slide-leave-active{
    animation: slideOut 1s;
    position: absolute;
    top:0;
    left: 0;
}

@keyframes slideOut {
    from{
      opacity: 1;
    }
    to{
      opacity: 0;
    }
}

@keyframes slideIn {
    from{
      opacity: 0;
    }
    to{
      opacity: 1;
    }
}
.animate-right-enter-active{
      -webkit-animation: animateRightIn .5s forwards;
}
.animate-right-before-enter{
    width: 100% !important;
}
.animate-right-leave-active {
    -webkit-animation: animateRightOut .5s forwards;
    position: absolute;
}
.animate-left-enter-active{
    -webkit-animation: animateLeftIn .5s forwards;
}
.animate-left-leave-active{
    -webkit-animation: animateLeftOut .5s forwards;
    position: absolute;
}
@-webkit-keyframes animateRightIn {
    0%{
      -webkit-transform: translate3d(100%,0,0);
    }
    100%{
      -webkit-transform: translate3d(0,0,0);

    }
}
@-webkit-keyframes animateRightOut {
    0%{
      -webkit-transform: translate3d(0,0,0);
    }
    100%{
      -webkit-transform: translate3d(-100%,0,0);
    }
}
@-webkit-keyframes animateLeftIn {
    0%{
      -webkit-transform: translate3d(-100%,0,0);
    }
    100%{
      -webkit-transform: translateX(0);
    }
}
@-webkit-keyframes animateLeftOut {
    0%{
      -webkit-transform: translateX(0);
    }
    100%{
      -webkit-transform: translateX(100%);
    }
}
</style>
