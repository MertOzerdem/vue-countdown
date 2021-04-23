<template>
  <div class="timer-inputs">Enter Time:
    <input v-model="year" placeholder="Year">
    <input v-model="month" placeholder="month">
    <input v-model="date" placeholder="date">
    <input v-model="hour" placeholder="hour">
    <input v-model="minute" placeholder="minute">
    <input v-model="second" placeholder="second">
    <input v-model="millisecond" placeholder="millisecond">
  </div>
  <div class="home">
    <Counter
    :year="year"
    :month="month"
    :date="date"
    :hour="hour"
    :minute="minute"
    :second="second"
    :millisecond="millisecond">
    </Counter>
  </div>
</template>

<script>
import Counter from '@/components/Counter.vue'

export default {
  name: 'Home',
  components: {
    Counter
  },
  data: function () {
    return {
      year: '2021',
      month: '11',
      date: '13',
      hour: '1',
      minute: '1',
      second: '1',
      millisecond: '1'
    }
  }
}
</script>

<style scoped>
.timer-inputs {
  display: flex;
  flex-direction: column;
  align-items: center;
}

input {
  display: block;
  margin: 5px 0px;
}
</style>
