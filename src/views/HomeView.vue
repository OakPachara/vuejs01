<script setup>
import TheWelcome from '../components/TheWelcome.vue'
</script>

<script>
export default {
  name: 'MyComponent',
  data() {
    return {
      latestTrickTime: 0
    }
  },
  mounted() {
    this.intervalFunction() // Initial execution
    setInterval(this.intervalFunction, 10000) // 10 seconds
  },
  methods: {
    intervalFunction() {
      const currentDate = new Date()
      const hours = currentDate.getHours()
      const minutes = currentDate.getMinutes()
      const seconds = currentDate.getSeconds()
      const formattedDate = `Interval - ${hours}:${minutes}:${seconds}`

      const currentTime = hours * 3600 + minutes * 60 + seconds
      const timeDifference = this.latestTrickTime === 0 ? 0 : currentTime - this.latestTrickTime

      if (timeDifference <= 12)
        console.log(`${formattedDate} - Time Difference: ${timeDifference} sec`)
      else console.warn(`${formattedDate} - Time Difference: ${timeDifference} sec`)

      this.latestTrickTime = currentTime
    }
  }
}
</script>

<template>
  <main>
    <TheWelcome />
  </main>
</template>
