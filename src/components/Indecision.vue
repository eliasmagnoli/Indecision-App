<template>
  <img class="gif" v-if="img" :src="img" alt="bg">
  <div class="bg-dark"></div>

  <div class="indecision-container">

    <input type="text" v-model="question">
    <p>Recuerda terminar con una interrogación (?)</p>

    <div v-if="isValidQuestion">
      <h2>{{question}}</h2>
      <h1>{{answer}}</h1>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      question: null,
      answer: null,
      img: null,
      isValidQuestion: false
    }
  },
  methods: {
    async getAnswer() {

      this.answer = "Pensando..."

      const {answer, image} = await fetch("https://yesno.wtf/api").then(r => r.json())

      this.answer = answer === "yes" ? "Si" : "No"
      this.img = image
    }
  },
  watch: {
    question(value, oldValue) {

      this.isValidQuestion = false

      if (!value.includes("?")) return

      this.isValidQuestion = true

      
      //TODO: Realizar peticion http
      this.getAnswer()
    }
  }
  
}
</script>

<style scoped>

    .gif{
        height: 100vh;
        left: 0px;
        max-height: 100%;
        max-width: 100%;
        position: fixed;
        top: 0px;
        width: 100vw;
        z-index: 80;
    }
     .bg-dark {
        height: 100vh;
        left: 0px;
        max-height: 100%;
        max-width: 100%;
        position: fixed;
        top: 0px;
        width: 100vw;
        z-index: 70;
    }

    .bg-dark {
        background: url(../assets/pexels-future-kiiid-3828760.jpg);
    }

    .indecision-container {
        position: relative;
        z-index: 99;
        height: 90vh;
        flex-direction: column;
        display: flex;
        align-items: center;
        justify-content: center;
        overflow: hidden;
        gap: 1rem;
    }
    
    input {
        width: 250px;
        padding: 10px 15px;
        border-radius: 20px;
        border: none;
        background-color: transparent;
        outline: 2px solid #d7d7d7
    }
    input:focus {
        outline: none;
        background: #d7d7d7;
        color: #101010;
    }

    p {
        color: #d7d7d7;
        font-family: Verdana, Geneva, Tahoma, sans-serif;
        font-size: 20px;
        margin-top: 0px;
    }

    h1, h2 {
        color: #d7d7d7;
    }
    
    h2 {
        margin-top: 150px;
    }

</style>