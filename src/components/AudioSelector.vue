<template>
    <div>
      <label for="audio-select">Audio Files: </label>
      <select id="audio-select" v-model="selectedAudio" @change="emitAudioSelection">
        <option v-if="audioFiles.length === 0" disabled>No audio files available</option>
        <option v-for="audio in audioFiles" :key="audio.file_name" :value="audio.storage_url">
    {{ audio.file_name }}
  </option>
</select>
    </div>
  </template>
  
<script>
export default {
  data() {
    return {
      selectedAudio: '',
      audioFiles: []
    };
  },
  methods: {
    emitAudioSelection() {
      this.$emit('audio-selected', this.selectedAudio);
    },
    async fetchAudioSelection() {
      console.log("Fetching audio files...");
      try {
        const response = await fetch('https://audio-app-api.onrender.com/api/audio-files');
        if (!response.ok) {
          throw new Error('API network response was not ok');
        }
        const data = await response.json();
        console.log('Fetched audio files:', data); // Log the raw data
        this.audioFiles = data.map(audio => ({
          file_name: audio.file_name,
          storage_url: audio.storage_url
        }));
        console.log('Mapped audio files:', this.audioFiles); // Log the mapped array
      } catch (error) {
        console.error('Error fetching audio files', error);
      }
    }
  },
  mounted() {
    this.fetchAudioSelection();
  }
};
</script>