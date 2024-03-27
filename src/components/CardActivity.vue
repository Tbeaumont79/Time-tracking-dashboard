<script setup lang="ts">
import { defineProps } from 'vue'
defineProps({
  activity: {
    type: Object,
    required: true
  },
  timeFilter: {
    type: String,
    required: true
  }
})
</script>
<template>
  <div class="card">
    <div class="card-info">
      <div class="title">
        <p>{{ activity.title }}</p>
        <img src="../assets/images/icon-ellipsis.svg" alt="three dots" />
      </div>
      <div class="content-card">
        <h2 v-if="timeFilter === 'Daily'">{{ activity.timeframes.daily.current }}hrs</h2>
        <h2 v-if="timeFilter === 'Weekly'">{{ activity.timeframes.weekly.current }}hrs</h2>
        <h2 v-if="timeFilter === 'Monthly'">{{ activity.timeframes.monthly.current }}hrs</h2>
        <p v-if="timeFilter === 'Daily'">Last Day - {{ activity.timeframes.daily.previous }}hrs</p>
        <p v-if="timeFilter === 'Weekly'">
          Last Week - {{ activity.timeframes.weekly.previous }}hrs
        </p>
        <p v-if="timeFilter === 'Monthly'">
          Last Month - {{ activity.timeframes.monthly.previous }}hrs
        </p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card {
  height: 100%;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}
.card-info {
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  align-items: flex-start;
  padding: 1rem;
}
.title {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
}
.content-card {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 100%;
}
.content-card h2 {
  font-size: 1.6rem;
  color: var(--color-heading);
}
.content-card p {
  color: var(--color-secondary);
}
@media screen and (min-width: 1440px) {
  .content-card {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: flex-start;
    height: 100%;
  }
  .content-card h2 {
    font-size: 2.5rem;
  }
}
</style>
