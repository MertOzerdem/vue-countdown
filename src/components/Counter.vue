<template>
    <div v-if="loaded" class="display-box" >
        <div class="display-number days">
            {{displayDays}}
        </div>
        <div class="display-number hours">
            {{displayHours}}
        </div>
        <div class="display-number minutes">
            {{displayMinutes}}
        </div>
        <div class="display-number seconds">
            {{displaySeconds}}
        </div>
    </div>
</template>

<script>
export default {
  props: ['year', 'month', 'date', 'hour', 'minute', 'second', 'millisecond'],
  data: function () {
    return {
      displayDays: 0,
      displayHours: 0,
      displayMinutes: 0,
      displaySeconds: 0,
      loaded: false
    }
  },
  computed: {
    seconds: function () {
      return 1000
    },
    minutes: function () {
      return this.seconds * 60
    },
    hours: function () {
      return this.minutes * 60
    },
    days: function () {
      return this.hours * 24
    },
    end () {
      return new Date(
        this.year,
        this.month,
        this.date,
        this.hour,
        this.minute,
        this.second,
        this.millisecond
      )
    }
  },
  methods: {
    formatTime: (number) => number < 10 ? '0' + number : number,
    resetTimer (timer) {
      const now = new Date()
      const distance = this.end - now.getTime()

      if (distance < 0) {
        clearInterval(timer)
        return
      }

      const days = Math.floor((distance / this.days))
      const hours = Math.floor((distance % this.days) / this.hours)
      const minutes = Math.floor((distance % this.hours) / this.minutes)
      const seconds = Math.floor((distance % this.minutes) / this.seconds)
      this.displayMinutes = this.formatTime(minutes)
      this.displaySeconds = this.formatTime(seconds)
      this.displayHours = this.formatTime(hours)
      this.displayDays = this.formatTime(days)

      this.loaded = true
    },
    showRemaining () {
      const timer = setInterval(() => {
        this.resetTimer(timer)
      }, 1000)
    }
  },
  mounted () {
    this.showRemaining()
  }

}
</script>

<style scoped>
.display-box {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
}

.display-number{
    font-size: 75px;
    font: bold;
}

.display-number:not(:last-child)::after {
    content: ':'
}
</style>
