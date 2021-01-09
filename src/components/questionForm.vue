<template>
  <div>
    <div class="main">
      <h1>Fråga {{ currentState }}</h1>
      <p>{{ getQuestion }}</p>
    </div>
    <div class="input">
      <p>Skriv ditt svar</p>
      <div>
        <input type="text" v-model="input" /><br />
        <input v-if="currentState === 1" type="text" v-model="inputTwo" /><br />
        <button @click="answer">Svara</button>
      </div>
    </div>
    <div class="response">
      <div v-if="response === true">
        <p>Det är rätt Svar! Jihooo!!!</p>
        <button @click="goToClue">Gå till ledtråd</button>
      </div>
      <div v-if="response === false">
        <p>Det är fel! Försök igen</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    currentState: {
      type: Number,
    },
  },
  data() {
    return {
      input: "",
      inputTwo: "",
      response: "",
    };
  },
  computed: {
    getQuestion() {
      if (this.currentState === 1) {
        return "Pappans och sonens ålder är tillsammans 66 år. Pappans ålder är densamma som sonens, men med siffrorna omvänt. Hur gamla är de?";
      } else if (this.currentState === 2) {
        return "Jag fyllde 12 år igår. Nästa år fyller jag 14 år. När är jag född? Svara med dag och månad, t.ex 6 juli ";
      } else if (this.currentState === 3) {
        return "Hur många amerikanska stater gränsar till Mexikanska golfen? ";
      } else if (this.currentState === 4) {
        return "Vilken utforskare introducerade grisar till Nordamerika? ";
      } else if (this.currentState === 5) {
        return "Om Patrick fick välja ett språk som han skulle kunna prata flytande, vilket språk skulle det då vara? ";
      }
      return "hej";
    },
  },
  methods: {
    answer() {
      event.preventDefault();
      if (this.currentState === 1) {
        this.answerOne();
      } else if (this.currentState === 2) {
        this.answerTwo();
      } else if (this.currentState === 3) {
        this.answerThree();
      } else if (this.currentState === 4) {
        this.answerFour();
      } else if (this.currentState === 5) {
        this.answerFive();
      }
      if (this.input.toLowerCase() == "x") {
        this.response = true;
      }
    },
    answerOne() {
      const answer = [
        [51, 15],
        [42, 24],
        [60, 6],
      ];
      answer.forEach((el) => {
        console.log(el);
        if (
          (el[0] == this.input && el[1] == this.inputTwo) ||
          (el[1] == this.input && el[0] == this.inputTwo)
        ) {
          this.response = true;
        }
      });
      if (this.response === "") {
        this.response = false;
      }
    },
    answerTwo() {
      const answer = "31 december";
      if (this.input.toLowerCase() === answer) {
        this.response = true;
      } else {
        this.response = false;
      }
    },
    answerThree() {
      if (this.input == 5 || this.input.toLowerCase() == "fem") {
        this.response = true;
      } else {
        this.response = false;
      }
    },
    answerFour() {
      const answer = "christopher columbus";
      if (this.input.toLowerCase() === answer) {
        this.response = true;
      } else {
        this.response = false;
      }
    },
    answerFive() {
      const answer = "koreanska";
      if (this.input.toLowerCase() === answer) {
        this.response = true;
      } else {
        this.response = false;
      }
    },
    goToClue() {
      this.$emit("go-to-clue");
    },
  },
};
</script>

<style scoped>
.main {
  width: 80%;
  max-width: 400px;
  height: 50vh;
  margin: 0 auto;
  background-color: rgb(218, 218, 218);
  border-radius: 5px;
}
input {
  width: 80%;
  max-width: 400px;
  border-radius: 5px;
}
</style>