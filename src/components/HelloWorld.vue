<template>
  <div>
    <button class="big-button" @click="startSpeechToTxt">Play me!</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      runtimeTranscription_: "",
      transcription_: [],
      lang_: "fr-FR",
    };
  },
  methods: {
    startSpeechToTxt() {
      // start speech to txt
      var utterance = new SpeechSynthesisUtterance(
        "Buenos días Patxi! Qué tal estas? Hoy es un buen día para programar. adios!"
      );
      utterance.lang = "es-ES";
      utterance.rate = -2;
      console.log(utterance);
      window.speechSynthesis.speak(utterance);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
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
