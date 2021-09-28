<template>
  <div id="app"
  class="recorder">

    <div class="recorder__header">
      <h1 class="recorder__h1">screen recorder</h1>
    
      <div class="recorder__buttons">

        <button class="recorder__btn"
          v-if="!isRecording"
          @click="startRecording()">
          Start recorder
        </button>

        <button class="recorder__btn"
          v-if="isRecording"
          @click="stopRecording()">
          Stop
        </button>

      </div>
    </div>


    <div class="recorder__wrapper">
      <div class="recorder__footer" v-if="isRecording">

        <video 
        class="recorder__video"
        src=""
        controls="controls"></video>

        <button class="recorder__btn"
          @click="downloadVideo()">
          Download
        </button>

      </div>
    </div>

  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      isRecording: false,
      options: { mimeType: 'video/webm' },
      displayMediaOptions: {
        video: {
          cursor: "always",
          logicalSurface: false
        },
        audio: {
          echoCancellation: false,
          noiseSuppression: false,
          sampleRate: 44100
        }
      },
      recordedChunks: [],
      stream: {},
      mediaRecorder: {}
    }
  },
  methods: {
    async startRecording() {
      this.isRecording = true;
      
      this.stream = await navigator.mediaDevices.getDisplayMedia(this.displayMediaOptions);
      this.mediaRecorder = new MediaRecorder(this.stream, this.options);
      this.mediaRecorder.ondataavailable = this.handleDataAvailable;
      this.mediaRecorder.start();

    },
    handleDataAvailable(event) {
      if (event.data.size > 0) {
        this.recordedChunks.push(event.data);
      }
    },
    stopRecording() {
      this.isRecording = false;
      
      this.mediaRecorder.stop();
    }
  }
}
</script>

<style lang="scss">
body {
  background: #1b2631;
  font-family: Arial, Helvetica, sans-serif;
}
.recorder {
  &__h1 {
    font-size: 45px;
    letter-spacing: 3px;
    color: #f1c40f;
    text-align: center;
  }

  &__buttons {
    display: flex;
    justify-content: center;
  }

  &__btn {
    display: block;
    background: #1b2631;
    margin: 10px auto;
    padding: 10px 30px;
    border: 2px solid #f1c40f;
    color: #f1c40f;
    font-family: Arial, Helvetica, sans-serif;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: 600;
    cursor: pointer;
    transition: 0.8s;

    &:hover {
      background: #f1c40f;
      color: #1b2631;
    }
  }

  &__video {
    display: block;
    width: 50%;
    margin: 30px auto;
  }
}
</style>
