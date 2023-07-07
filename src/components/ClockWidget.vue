<template>
  <div class="clock-widget">
    <h2 class="widget-title">Clock Widget</h2>
    <div class="clock">
      <div class="time">{{ currentTime }}</div>
      <div class="date">{{ currentDate }}</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentTime: '',
      currentDate: ''
    };
  },
  mounted() {
    this.updateTime();
    setInterval(() => {
      this.updateTime();
    }, 1000);
  },
  methods: {
    updateTime() {
      const now = new Date();
      this.currentTime = now.toLocaleTimeString('en-US', { hour: 'numeric', minute: 'numeric', second: 'numeric' });
      this.currentDate = now.toLocaleDateString('en-US', { weekday: 'long', month: 'long', day: 'numeric', year: 'numeric' });
    }
  }
};
</script>

<style>
.clock-widget {
  max-width: 300px;
  margin: auto;
  font-family: 'Courier New', monospace;
  text-align: center;
}

.widget-title {
  font-size: 20px;
  font-weight: bold;
}

.clock {
  width: 100%;
  border: 1px solid #ccc;
  padding: 10px;
}

.time {
  font-size: 32px;
  font-weight: bold;
  margin-bottom: 10px;
}

.date {
  font-size: 18px;
}
</style>
