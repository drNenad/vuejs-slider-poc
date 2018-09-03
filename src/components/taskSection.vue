<template>
  <div class="contentSection">
    <h2>{{heading}}</h2>
    <ul>
      <li
        v-for="(list, index) in lists"
      >
        <label>
          <input type="checkbox" @click="test($event)" :id="index" :checked="list.checked"/>
          {{list.title}}
        </label>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    props: ['heading','lists','list'],
    methods: {
      test(event){
        this.$emit('test', event)
      }
    }
  }
</script>
