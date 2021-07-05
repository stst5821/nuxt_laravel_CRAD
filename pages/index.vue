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
    <!-- <div>
      <p>{{ $store.state.results }}</p>
    </div> -->
    <ul>
      <li v-for="result in results" :key="result.id">
        <!-- <li v-for="result in $store.state.results" :key="result.id"> -->
        id:{{ result.id }} | name:{{ result.name }} | 本文:{{ result.body }}
        <button @click="remove(result.id)">X</button>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'
// import { mapState } from 'vuex'

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
    // laravelのPostControllerのstoreにデータを送る。
    submit() {
      const CORS_PROXY = 'http://localhost/'
      // DBへの登録が完了したら、getでDBからデータを取ってきて追加したデータを画面に表示させる。
      axios.post(CORS_PROXY + 'api/store', { name: this.name }).then(() => {
        axios.get(CORS_PROXY + 'api/test1').then((response) => {
          this.results = response.data.result
          console.log(this.results)
        })
      })
    },
    remove(id) {
      const CORS_PROXY = 'http://localhost/'
      axios.post(CORS_PROXY + 'api/delete', { id }).then(() => {
        axios.get(CORS_PROXY + 'api/test1').then((response) => {
          this.results = response.data.result
          console.log(this.results)
        })
      })
    },
  },
}
</script>
