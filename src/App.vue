<template>
  <div id="app" class="app-background">
    <h1 class="center-text text-color"> Basic Audio Player</h1>
    <AudioSelector @audio-selected="updateAudio" />
    <AudioPlayer :key="currentAudio" :audio-url="currentAudio" />
  </div>
</template>

<script>
import AudioPlayer from './components/AudioPlayer.vue';
import AudioSelector from './components/AudioSelector.vue';

export default {
  name: 'App',
  components: {
    AudioPlayer,
    AudioSelector
  },
  data() {
    return {
      currentAudio: ''
    };
  },
  methods: {
    updateAudio(selectedAudio) {
      this.currentAudio = selectedAudio;
    }
  }
};
</script>

<style>
.app-background {
  background-color: #c3b091; /* Gloss khaki */
  height: 100vh;
  border: 8px solid #00004d;
  display: flex; /* Keeps the layout flexible */
  flex-direction: column; /* Stacks elements vertically */
  align-items: center; /* Centers children horizontally */
}

.center-text {
  text-align: center; /* Centers the text horizontally */
  margin: 0; /* Removes any default margin */
}

.text-color {
  color: #00004d;
  text-decoration: underline;
}
</style>