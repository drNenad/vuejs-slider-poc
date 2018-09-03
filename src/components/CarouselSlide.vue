<template>
    <div v-show="visible"  :style="{'width':'calc(100%/'+this.$parent.numOfSlides+')'}">
      <slot></slot>
    </div>
</template>

<script>
  export default {
    props: ['id','slidescount'],
    data(){
      return{
        index : 0,
      }
    },
    computed: {
      visible(){
        if(Array.isArray(this.$parent.index)){
            for(var i=0; i < this.$parent.index.length; i++){
            if( this.$parent.index[i] == this.index){
            return true

             }
          }
      }
        else{
            return this.id === this.$parent.index
        }
      },
    }
  }
</script>

<style scoped>
.slider{
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
}
.text-wrapper{
  position: absolute;
  text-align: center
}
</style>

