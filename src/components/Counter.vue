<template>
  <h2>{{ customTitle }}</h2>
  <p>{{ counter }}</p>

  <button @click="increaseOne()">+1</button>
  <button @click="decreaseOne()">-1</button>
</template>

<script>
export default {
  props: {
    title: String,
    start:{
      type: Number,
      default: 1,
      // required: true
      validator(){
        
      }
    }
    
  },
  
  // name:"Cauner",

  data() {
    return {
      counter: this.start
    }
  },

  methods:{

    increaseOne(){
      this.counter++
    },

    decreaseOne(){
      this.counter--
    }
    
  },

  computed: {
    customTitle(){
       if (this.title === undefined) {
            return "Counter"
      } else {
            return this.title        
      }
    }
  }
}
</script>

<style>

  button{
    background-color: #64bb87;
    border-radius: 20px;
    border: 1px solid white;
    color: white;
    cursor: pointer;
    margin: 0 5px;
    padding: 5px 15px;
    transition: 0.3s ease-in-out;
  }

  button:hover{
    background-color: #6cdd99;
    transition: 0.3s ease-in-out;
  }

</style>