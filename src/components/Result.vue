<template>
  <img :src="image" alt="Resultado">
  <p>{{rightAnswers}}/10</p>
</template>

<script>
import {ref} from "vue"

export default {
  name:"Result",
  props:{
    rightAnswers:Number
  },
  setup(props){
    let image = ref("/img/about.png")

    if(props.rightAnswers>8) image.value="/img/dani.png"
    else if(props.rightAnswers>6) image.value="/img/nuria.png"
    else if(props.rightAnswers>4) image.value="/img/home.png"

    return{
      image
    }
  }

}
</script>

<style lang="scss" scoped>

</style>