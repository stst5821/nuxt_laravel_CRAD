<template>
  <div>
    {{ result.id }}
    {{ result.name }}
    {{ result.body }}
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      result: '',
    }
  },
  mounted() {
    axios
      .get('http://localhost/test1')
      .then((response) => {
        this.result = response.data.result
        console.log(this.result)
      })
      .catch((error) => {
        console.log(error)
        this.result = 'ERROR'
      })
  },
}
</script>
