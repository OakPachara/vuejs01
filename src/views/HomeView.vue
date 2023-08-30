<script setup>
import TheWelcome from '../components/TheWelcome.vue'
</script>

<script>
import axios from 'axios'

export default {
  name: 'MyComponent',
  data() {
    return {
      latestTrickTime: 0
    }
  },
  mounted() {
    this.callAzureLogicApp() // Initial execution
    setInterval(this.callAzureLogicApp, 60000) // 60 seconds
  },
  methods: {
    getCurrentDate() {
      const currentDate = new Date()
      const hours = currentDate.getHours()
      const minutes = currentDate.getMinutes()
      const seconds = currentDate.getSeconds()
      const formattedDate = `Interval - ${hours}:${minutes}:${seconds}`

      const currentTime = hours * 3600 + minutes * 60 + seconds
      const timeDifference = this.latestTrickTime === 0 ? 0 : currentTime - this.latestTrickTime
      this.latestTrickTime = currentTime

      return `${formattedDate} - Time Difference: ${timeDifference} sec`
    },
    callAzureLogicApp() {
      axios
        .get(
          'https://prod-59.southeastasia.logic.azure.com:443/workflows/15724ec6420c46f8af7e5ee7b5dcae7d/triggers/request/paths/invoke?api-version=2016-10-01&sp=%2Ftriggers%2Frequest%2Frun&sv=1.0&sig=txoN2gzu9nG6hwWsjISvJ9u4OlmBbDU-djsSG9-wzB4'
        )
        .then((response) => {
          // Handle the response data here
          console.log(`${response.status} - ${this.getCurrentDate()}`)
        })
        .catch((error) => {
          // Handle any errors here
          console.error(error)
        })
    }
  }
}
</script>

<template>
  <main>
    <TheWelcome />
  </main>
</template>
