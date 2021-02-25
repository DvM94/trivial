<template>
  <div class="card" v-if="cardInfo.length">
    <div class="question">
      <p v-html="cardInfo[0].question"></p>
    </div>
    <div class="answers">
      <div class="bullets">
        <p>A</p>
        <p>B</p>
        <p>C</p>
        <p>D</p>
      </div>
      <div @click.once="checkAnswer($event)" id="answersList">
        <p
          v-for="(answer, i) in answers"
          :key="i"
          :id="`ans${i}`"
          v-html="answer"
        ></p>
      </div>
    </div>
  </div>
  <img src="/img/next.png" alt="Siguiente pregunta" @click="loadCard" @mouseover="hover($event,'/img/next2.png')" @mouseout="hover($event,'/img/next.png')"/>
</template>

<script>
import { ref, reactive } from "vue";
export default {
  name: "Card",
  emits: ["questionsNumber","correctAnswer"],
  props: {},
  setup(props, context) {
    let cardInfo = reactive([]);
    let answers = reactive([]);
    let correctAnswer = ref("");

    const decodeHTML = (text) => {
      let txt = document.createElement("textarea");
      txt.innerHTML = text;
      return txt.value;
    };

    const loadCard = () => {
      context.emit("questionsNumber");
      cardInfo.splice(0);
      answers.splice(0);
      fetch("https://opentdb.com/api.php?amount=1&category=9&type=multiple")
        .then((res) => res.json())
        .then((data) => {
          answers.push(...data.results[0].incorrect_answers);
          answers.splice(
            Math.round(Math.random() * 3),
            0,
            data.results[0].correct_answer
          );
          correctAnswer.value = decodeHTML(data.results[0].correct_answer);
          console.log(correctAnswer.value);
          cardInfo.push(data.results[0]);
        });
    };

    loadCard();

    const checkAnswer = (e) => {
      if (e.target.textContent == correctAnswer.value) {
        e.target.style.backgroundColor = "rgb(80, 199, 80)"
        context.emit("correctAnswer");
      } else {
        e.target.style.backgroundColor = "rgb(231, 98, 98)"
        Array.from(answersList.children).forEach((ans) => {
          if (ans.textContent == correctAnswer.value)
            ans.style.backgroundColor = "rgb(80, 199, 80)"
        });
      }
    };

    const hover = (e,link) => e.target.src = link

    return {
      hover,
      cardInfo,
      answers,
      checkAnswer,
      loadCard,
    };
  },
};
</script>

<style lang="scss" scoped>
.card {
  width: 100%;
  background-color: rgb(179, 177, 177);
  box-shadow: 3px 3px 5px gray;
  border: 1px solid black;
  border-radius: 10px;
  padding: 25px 0;
}
.question {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 0 30px 25px;
  border-radius: 10px 10px 0 0;

  p {
    font-size: 1.3rem;
    font-weight: 700;
    color: #4b72a6;
    text-shadow: 1px 0 0 #000, -1px 0 0 #000, 0 1px 0 #000, 0 -1px 0 #000, 1px 1px #000, -1px -1px 0 #000, 1px -1px 0 #000, -1px 1px 0 #000;
    text-align: center;
    letter-spacing: 4px;
    line-height: 30px;
  }
}

.answers {
  display: flex;
  justify-content: space-between;
  padding: 0 50px;
  font-size: 1.1rem;

  p {
    text-align: center;
    font-weight: 700;
    color: white;
    line-height: 40px;
    border-radius: 50%;
    margin-bottom: 10px;
    border: 1px solid black;
    background-color: #68a0e9;
  }

  .bullets {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    width: 13%;

    p:nth-child(2) {
      background-color: #fdbd33;
    }

    P:nth-child(3) {
      background-color: #ff6f69;
    }

    p:last-child {
      background-color: #4ed496;
    }
  }

  #answersList {
    width: 85%;
    cursor: pointer;
    font-weight: bold;
    font-size: 1rem;
    letter-spacing: 1px;

    p {
    color: rgb(71, 71, 71);
    border-radius: 10px;
    background-color:rgba(255, 255, 255, 0.466);
    }

    P:hover {
      background-color: white;
    }
  }
}

img {
  display: block;
  margin: 15px auto;
  width: 45%;
}

@media (max-width: 600px) {
  .card {
    padding: 15px 0;
  }

  .question {
    padding: 0 10px 15px;

    p {
      font-size: 1.1rem;
      font-weight: 700;
      letter-spacing: 2px;
      line-height: 25px;
    }
  }

  .answers {
    padding: 0 10px;
    font-size: 0.9rem;

    .bullets {
      width: 13%;

      p {
        line-height: 30px;
      }
    }

    #answersList {
      font-size: 0.8rem;
      letter-spacing: 0;

      p {
        line-height: 30px;
      }
    }
  }

  img {
  width: 60%;
  }
}
</style>