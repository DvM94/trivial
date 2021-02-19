<template>
<div class="card" v-if="cardInfo.length">
  <p v-html="cardInfo[0].question"></p>
  <p v-for="(answer, i) in answers" :key="i" :id="`ans${i}`" v-html="answer" @click.once="checkAnswer($event,answer)"></p>
</div>

</template>

<script>
import{ ref,reactive } from "vue"
export default {
  name:"Card",
  props:{},
  setup(){
    let cardInfo = reactive([])
    let answers = reactive([])
    let correctAnswer = ref("")
    
    console.log(cardInfo)
    
    fetch("https://opentdb.com/api.php?amount=1&difficulty=easy&type=multiple")
      .then(res=>res.json())
      .then(data=>{
        answers.push(...data.results[0].incorrect_answers)
        answers.splice(Math.round(Math.random()*3),0,data.results[0].correct_answer)
        correctAnswer.value = data.results[0].correct_answer
        cardInfo.push(data.results[0])
      })
    
    const checkAnswer = (e,answer) => {
      if(answer==correctAnswer.value)
        e.target.classList.add("right")
      else
        e.target.classList.add("wrong")
    }

    return{
      cardInfo,
      answers,
      checkAnswer
    }
  }
}
</script>

<style lang="scss" scoped>
.right{
  background-color: green;
}
.wrong{
  background-color: red;
}
</style>