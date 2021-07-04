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
    <ul>
      <li v-for="result in results" :key="result.id">
        id:{{ result.id }} | name:{{ result.name }} | 本文:{{ result.body }}
        <button @click="remove(result.id)">X</button>
      </li>
    </ul>
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
      const CORS_PROXY = 'http://localhost/'
      axios.post(CORS_PROXY + 'api/store', { name: this.name })
    },
    remove(id) {
      const CORS_PROXY = 'http://localhost/'
      axios.post(CORS_PROXY + 'api/delete', { id })
      console.log(id)
    },
  },
}
</script>
