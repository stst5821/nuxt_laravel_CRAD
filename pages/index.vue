<template>
  <div>
    <div v-for="result in results" :key="result.id">
      {{ result.id }}
      {{ result.name }}
      {{ result.body }}
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      results: '',
    }
  },
  mounted() {
    axios
      .get('http://localhost/test1')
      .then((response) => {
        this.results = response.data.result
        console.log(this.results)
      })
      .catch((error) => {
        console.log(error)
        this.result = 'ERROR'
      })
  },
}
</script>
