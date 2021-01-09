<template>
  <div class="main">
    <div v-if="currentState === 0">
      <button class="big-button" @click="startSpeechToTxt">Spela mig!</button>
      <div>
        <button class="lets-go" @click="go">Let's go!</button>
        <audio v-show="false" id="AudioTag" controls>
          <source src="./../assets/mario.mp3" type="audio/mpeg" />
          Your browser does not support the audio element.
        </audio>
      </div>
    </div>
    <div v-if="currentState === 1">
      <questionForm
        v-if="!showClue"
        :currentState="currentState"
        @go-to-clue="showClue = true"
      />
      <div v-if="showClue">
        <p>
          Din första present ligger i en låda i köket, där du inte visste att du
          hade köksredskap fören jag visade dig
        </p>
        <button @click="changeState">nästa fråga</button>
      </div>
    </div>
    <div v-if="currentState === 2">
      <questionForm
        v-if="!showClue"
        :currentState="currentState"
        @go-to-clue="showClue = true"
      />
      <div v-if="showClue">
        <p>Ditt andra paket kan du hitta i din julklapp.</p>
        <button @click="changeState">nästa fråga</button>
      </div>
    </div>
    <div v-if="currentState === 3">
      <questionForm
        v-if="!showClue"
        :currentState="currentState"
        @go-to-clue="showClue = true"
      />
      <div v-if="showClue">
        <p>Ditt tredje paket finner du där jag brukar lägga mina kläder</p>
        <button @click="changeState">nästa fråga</button>
      </div>
    </div>
    <div v-if="currentState === 4">
      <questionForm
        v-if="!showClue"
        :currentState="currentState"
        @go-to-clue="showClue = true"
      />
      <div v-if="showClue">
        <p>Ditt fjärde paket kan du hitta där vi förvarar vår Huel</p>
        <button @click="changeState">nästa fråga</button>
      </div>
    </div>
    <div v-if="currentState === 5">
      <questionForm
        v-if="!showClue"
        :currentState="currentState"
        @go-to-clue="showClue = true"
      />
      <div v-if="showClue">
        <p>
          Ditt femte paket hittar du på den kyligaste platsen hos dig (inte kyl
          eller frys).
        </p>
        <button @click="changeState">Avsluta</button>
      </div>
    </div>
    <div v-if="currentState === 6">
      <h1>STORT GRATTIS PÅ FÖDELSEDAGEN!</h1>
    </div>
  </div>
</template>

<script>
import questionForm from "./questionForm.vue";
export default {
  components: {
    questionForm,
  },
  data() {
    return {
      currentState: 0,
      showClue: false,
    };
  },
  methods: {
    startSpeechToTxt() {
      // start speech to txt

      var utterance = new SpeechSynthesisUtterance(
        "Hola Patchi, Hoy es tu cumpleaños y tienes paquetes esperándote. Para encontrar tus paquetes, tienes que responder diferentes tipos de preguntas y luego obtener una pista que te ayude a encontrar los paquetes. ¡Buena suerte!"
      );
      utterance.lang = "es";
      utterance.rate = 0;
      console.log(utterance);
      window.speechSynthesis.speak(utterance);
    },
    go() {
      document.getElementById("AudioTag").play();
      setTimeout(() => {
        this.changeState();
      }, 2000);
    },
    changeState() {
      this.showClue = false;
      this.currentState++;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.lets-go {
  margin-top: 4rem;
}
button {
  position: relative;
  display: inline-block;
  cursor: pointer;
  outline: none;
  border: 0;
  vertical-align: middle;
  text-decoration: none;
  font-size: 1.5rem;
  color: rgb(106, 163, 137);
  font-weight: 700;
  text-transform: uppercase;
  font-family: inherit;
}

button.big-button {
  padding: 1em 2em;
  border: 2px solid (rgb(106, 163, 137));
  border-radius: 1em;
  background: rgb(205, 255, 232);
  transform-style: preserve-3d;
  transition: all 175ms cubic-bezier(0, 0, 1, 1);
}
button.big-button::before {
  position: absolute;
  content: "";
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgb(150, 232, 195);
  border-radius: inherit;
  box-shadow: 0 0 0 2px rgb(121, 186, 156), 0 0.75em 0 0 (rgb(106, 163, 137));
  transform: translate3d(0, 0.75em, -1em);
  transition: all 175ms cubic-bezier(0, 0, 1, 1);
}

button.big-button:hover {
  background: rgb(187, 232, 211);
  transform: translate(0, 0.375em);
}

button.big-button:hover::before {
  transform: translate3d(0, 0.75em, -1em);
}

button.big-button:active {
  transform: translate(0em, 0.75em);
}

button.big-button:active::before {
  transform: translate3d(0, 0, -1em);

  box-shadow: 0 0 0 2px (--colorShadeB), 0 0.25em 0 0 (--colorShadeB);
}
</style>
