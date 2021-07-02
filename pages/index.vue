<template>
  <div>
    <form @submit.prevent>
      <label
        >入力：
        <input
          v-model="name"
          placeholder="入力ください"
          type="text"
          name="entry"
          @keyup.enter="submit"
        />
      </label>
      <button type="submit" @click="submit">送信</button>
    </form>

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
      name: '',
    }
  },
  mounted() {
    axios
      .get('http://localhost/api/test1')
      .then((response) => {
        this.results = response.data.result
        console.log(this.results)
      })
      .catch((error) => {
        console.log(error)
        this.result = 'ERROR'
      })
  },
  methods: {
    submit() {
      // const submitParams = new FormData()
      // submitParams.append('entry', this.name)
      const CORS_PROXY = 'http://localhost/'
      const name = this.name
      console.log(name)
      axios.post(CORS_PROXY + 'api/store', { name })
    },
  },
  // addData() {
  //   axios
  //     .post('http://localhost/store', {
  //       name: '送る名前',
  //     })
  //     .then(function (response) {
  //       // this.name = response.name
  //       console.log(response.data)
  //     })
  // },
}
</script>
