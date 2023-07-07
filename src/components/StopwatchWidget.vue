<template>
  <div class="stopwatch-widget">
    <h2>Stopwatch</h2>
    <p class="time">{{ formatTime }}</p>
    <div class="buttons">
      <button class="start-button" @click="startStopwatch" :disabled="isRunning">Start</button>
      <button class="stop-button" @click="stopStopwatch" :disabled="!isRunning">Stop</button>
      <button class="reset-button" @click="resetStopwatch">Reset</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isRunning: false,
      startTime: null,
      elapsedTime: 0,
    };
  },
  computed: {
    formatTime() {
      const minutes = Math.floor(this.elapsedTime / 60000);
      const seconds = Math.floor((this.elapsedTime % 60000) / 1000);
      const milliseconds = Math.floor((this.elapsedTime % 1000) / 10);

      return `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}.${milliseconds.toString().padStart(2, '0')}`;
    },
  },
  methods: {
    startStopwatch() {
      if (!this.isRunning) {
        this.isRunning = true;
        this.startTime = Date.now();

        this.timerInterval = setInterval(() => {
          this.elapsedTime = Date.now() - this.startTime;
          if (this.elapsedTime >= 3600000) {
            this.stopStopwatch();
          }
        }, 10);
      }
    },
    stopStopwatch() {
      if (this.isRunning) {
        this.isRunning = false;
        clearInterval(this.timerInterval);
      }
    },
    resetStopwatch() {
      this.isRunning = false;
      clearInterval(this.timerInterval);
      this.elapsedTime = 0;
    },
  },
};
</script>

<style scoped>
.stopwatch-widget {
  border: 2px solid #ccc;
  padding: 20px;
  margin-bottom: 20px;
  background-color: #f2f2f2;
  text-align: center;
}

.stopwatch-widget h2 {
  color: #333;
  font-size: 24px;
  margin-bottom: 10px;
}

.stopwatch-widget p.time {
  color: #333;
  font-size: 28px;
  margin-bottom: 20px;
  font-family: 'Courier New', monospace;
}

.stopwatch-widget .buttons {
  display: flex;
  justify-content: center;
  gap: 10px;
}

.stopwatch-widget button {
  padding: 10px 20px;
  background-color: #007bff;
  color: #ffffff;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.stopwatch-widget button:hover {
  background-color: #ddd;
}

.stopwatch-widget button:disabled {
  background-color: #ccc;
  color: #999;
  cursor: not-allowed;
}
</style>
