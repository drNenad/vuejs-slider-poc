<template>
  <section class="insertTaskSection">
    <input name="test" class="newTaskInput" placeholder="Insert Task Name"  v-model="testtest" @keyup.enter="addNewTodo"/>
    <button @click="addNewTodo" :class="'primaryButton'">Add New Task</button>
  </section>
</template>

<script>
  export default {
    props: ['newText','array','inputText','primaryButton'],
    data(){
      return{
        newTodoText: '',
        testtest: 'test'
      }
    },
    methods:{
      addNewTodo(){

        if (this.testtest !== null && this.testtest !== ''){
          this.$emit('addNewTodo', this.testtest)
        }
        else {
          alert('Ukucajte lepo poruku')
        }
      }
    }
  }
</script>
