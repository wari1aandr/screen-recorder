<template>
  <div id="app"
  class="recorder">

    <div>
      <h1 class="recorder__h1">screen recorder</h1>
    
      <div class="recorder__buttons">

        <button class="recorder__btn"
          v-if="!isRecording"
          @click="handleBtn()">
          Start recorder
        </button>
        <button class="recorder__btn"
          v-if="isRecording"
          @click="handleBtn()">
          Stop
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
    }
  },
  methods: {
    handleBtn() {
      this.isRecording = !this.isRecording;
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
  display: flex;
  justify-content: center;

  &__h1 {
    font-size: 45px;
    letter-spacing: 3px;
    color: #f1c40f;
  }

  &__buttons {
    display: flex;
    justify-content: center;
  }

  &__btn {
    background: #1b2631;
    display: inline-block;
    margin: 10px 20px;
    padding: 10px 30px;
    position: relative;
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
}
</style>
