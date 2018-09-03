<template>
<div id="app">

  <carousel :autoplaySpeed="3000" class="carouselmini" :numOfSlides="1" animationstyle="slide">
      <carousel-slide v-for="item in channelsCarousel" class="slider" :key="item.id" :id="item.id" >
        <img :src="item.src">
        <div class="text-wrapper">
          <h3>{{item.emission}}</h3>
          <h4>{{item.day}}</h4>
          <button class="primaryButton">{{item.button}}</button>
        </div>
      </carousel-slide>
  </carousel>

  <h1 class="slider-heading">Channel Carousel</h1>

  <carousel :autoplaySpeed="2000" class="carouselmini" :numOfSlides="6" >
      <carousel-slide v-for="item in channelsCarousel" class="slider" :key="item.id" :id="item.id" >
        <img :src="item.src">
        <!-- <h3>{{item.emission}}</h3>
        <h4>{{item.day}}</h4>
        <button class="primaryButton">{{item.button}}</button> -->
      </carousel-slide>
  </carousel>

  <app-newtask @addNewTodo="test4" :array="todos"></app-newtask>

  <section class="main-section">
    <app-tasks heading="All Tasks" :lists="todos" @test="test2($event)"></app-tasks>
    <app-tasks heading="Done Tasks" :lists="doneTasks"  @test="test3($event)"></app-tasks>
  </section>
</div>
</template>

<script>
import newTask from './components/newTask.vue'
import taskSection from './components/taskSection.vue'
import Carousel from './components/Carousel.vue'
import CarouselSlide from './components/CarouselSlide.vue'




export default {
  name: 'app',
  props: ['lists','slider'],
  data(){
    return{
      newTodoText: '',
      doneTasks: [
        {
          id: 0,
          title: 'Ovo sam vec uradio',
          checked: true
        }
      ],
      todos: [
        {
          id: 0,
          title: 'Do the dishes',
          checked: false
        },
        {
          id: 1,
          title: 'Take out the trash',
          checked: false
        },
        {
          id: 2,
          title: 'Mow the lawn',
          checked: false
        }
      ],
      channelsCarousel: [
        {
          id: 0,
          src: 'src/assets/img/img1.jpg',
          emission: 'Emsija 1',
          day: 'Danas',
          hours: '14:00-15:00'
        },
        {
          id: 1,
          src: 'src/assets/img/img1.jpg',
          emission: 'Emsija 1',
          day: 'Danas',
          hours: '14:00-15:00'
        },
        {
          id: 2,
          src: 'src/assets/img/img1.jpg',
          emission: 'Emsija 1',
          day: 'Danas',
          hours: '14:00-15:00'
        },
        {
          id: 3,
          src: 'src/assets/img/img2.jpg',
          emission: 'Emsija 1',
          day: 'Danas',
          hours: '14:00-15:00'
        },
        {
          id: 4,
          src: 'src/assets/img/img2.jpg',
          emission: 'Emsija 1',
          day: 'Danas',
          hours: '14:00-15:00'
        },
        {
          id: 5,
          src: 'src/assets/img/img2.jpg',
          emission: 'Emsija 1',
          day: 'Danas',
          hours: '14:00-15:00'
        },
        {
          id: 6,
          src: 'src/assets/img/img3.jpg',
          emission: 'Emsija 1',
          day: 'Danas',
          hours: '14:00-15:00'
        },
        {
          id: 7,
          src: 'src/assets/img/img3.jpg',
          emission: 'Emsija 1',
          day: 'Danas',
          hours: '14:00-15:00'
        },
        {
          id: 8,
          src: 'src/assets/img/img3.jpg',
          emission: 'Emsija 1',
          day: 'Danas',
          hours: '14:00-15:00'
        },
      ],
      nextTodoId: 3,
      }
  },
  components: {
    'app-newtask': newTask,
    'app-tasks' : taskSection,
    'carousel': Carousel,
    'carousel-slide': CarouselSlide
  },
  methods: {
    test2: function (event) {
      this.doneTasks.push({
        title: event.target.parentElement.innerText,
        checked: true
      })
      console.log(event)

      this.todos.splice(event.target.id, 1);

    },
    test3: function (event) {
      this.todos.push({
        title: event.target.parentElement.innerText,
        checked: false
      })
      console.log(event)

      this.doneTasks.splice(event.target.id, 1);
    },
    test4 : function(event){
      var y=[]

      for(var i=0; i < this.todos.length; i++){
        var x= this.todos[i]
        y.push(x.title)
      }
      for(var i=0; i < this.doneTasks.length; i++){
        var z= this.doneTasks[i]
        y.push(z.title)
      }

      if (y.includes(event)){
        alert('Postoji task sa ovakvim imenom, unesite drugaciji naziv.')
      }
      else {
        this.todos.push({title: event})
      }
    }
  }
}
</script>

<style>
body{
    font-family: 'Open Sans', sans-serif;
    color: #34495e;
    background-color: #f9f9f9;
    margin: 0px;
    -webkit-transform: translate3d(0, 0, 0);
  }
h1{
    margin-top: 0px;
}
h3{
    color: #fff;
    font-size: 32px;
    font-weight: bold;
    margin: 0px 0px 5px 0px;
    text-shadow: rgb(0, 0, 0) 1px 1px 1px;
}
h4{
    color: #fff;
    font-size: 22px;
    font-weight: bold;
    margin: 0px 0px 15px 0px;
    text-shadow: rgb(0, 0, 0) 1px 1px 1px;
}
img{
    max-width: 100%;
    max-height: 100%;
    width: auto;
    height: auto;
}
  
.primaryButton{
    padding: 8px 20px;
    border: none;
    background-color: #2196F3;
    color: #fff;
    cursor: pointer;
}
.primaryButton:hover{
    -webkit-transition: all 200ms ease-in-out;
    -moz-transition: all 200ms ease-in-out;
    -ms-transition: all 200ms ease-in-out;
    -o-transition: all 200ms ease-in-out;
    transition: all 200ms ease-in-out;
    -webkit-box-shadow: 0px 0px 15px 0px rgba(66,184,131,0.2);
    -moz-box-shadow: 0px 0px 15px 0px rgba(66,184,131,0.2);
    box-shadow: 0px 0px 15px 0px rgba(66,184,131,0.2);
}
input{
    padding: 6px 20px;
}
.main-section{
    display: flex;
}
h2{
    margin: 0px 0px 30px 15px;
}
.contentSection{
    background: #fff;
    border-radius: 2px;
    display: inline-block;
    height: 100%;
    margin: 1rem;
    position: relative;
    padding: 15px 15px 45px 15px;
    width: 300px;
    -webkit-box-shadow: 0px 12px 39px 3px rgba(0,0,0,0.32);
    -moz-box-shadow: 0px 12px 39px 3px rgba(0,0,0,0.32);
    box-shadow: 0 10px 20px rgba(0,0,0,0.19), 0 6px 6px rgba(0,0,0,0.23);
}
.contentSection ul{
    list-style: none;
    padding-left: 0px;
    margin-bottom: 0px;
}
.contentSection ul li{
    padding: 15px;
    border-bottom: 1px solid #ddd;
}
.contentSection ul li label i{
    float: right;
}
.insertTaskSection{
    margin: 30px 0px 30px 15px;
}
.slider-heading{
  text-align: center;
  margin-top: 20px
}
</style>


