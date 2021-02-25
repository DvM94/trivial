<template>
  <h1>Score: {{rightAnswers}}/10</h1>
  <img :src="image" alt="Resultado">
</template>

<script>
import {ref} from "vue"

export default {
  name:"Result",
  props:{
    rightAnswers:Number
  },
  setup(props){
    let image = ref("/img/result0.png")

    if(props.rightAnswers>8) image.value="/img/result3.png"
    else if(props.rightAnswers>6) image.value="/img/result2.png"
    else if(props.rightAnswers>4) image.value="/img/result1.png"

    return{
      image
    }
  }

}
</script>

<style lang="scss" scoped>
h1{
  width: fit-content;
  margin: 0 auto;
  padding: 0 20px;
  border: 2px solid black;
  border-radius: 30px;
  font-weight: 100;
  letter-spacing: 2px;
  background-color: #4b72a6;
  color: white;
  text-shadow: 2px 0 0 #000, -2px 0 0 #000, 0 2px 0 #000, 0 -2px 0 #000, 2px 2px #000, -2px -2px 0 #000, 2px -2px 0 #000, -2px 2px 0 #000;
}
</style>