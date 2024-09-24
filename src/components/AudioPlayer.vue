


<template>
    <div>
      <audio ref="audio" v-if="audioUrl" controls>
        <source :src="audioUrl" type="audio/aac">
        Your browser does not support the audio element.
      </audio>
      <div v-if="audioUrl">
        <button @click="skip(-10)">-10s</button>
        <button @click="skip(10)">+10s</button>
      </div>
      <p v-else>Select an audio file to play.</p>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      audioUrl: {
        type: String,
        required: false
      }
    },
    methods: {
      skip(seconds) {
        const audio = this.$refs.audio;
        if (audio) {
          audio.currentTime = Math.max(0, audio.currentTime + seconds);
        }
      }
    }
  };
  </script>