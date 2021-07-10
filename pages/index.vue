<template>
  <div>
    <form @submit.prevent>
      <label
        >名前：
        <input
          v-model="name"
          placeholder="入力ください"
          type="text"
          name="entry"
          @keyup.enter="submit"
        />
      </label>
      <br />
      <label
        >本文：
        <input
          v-model="body"
          placeholder="入力ください"
          type="text"
          name="entry"
          @keyup.enter="submit"
        />
      </label>
      <button
        class="
          bg-blue-500
          hover:bg-blue-700
          text-white
          font-bold
          py-1
          px-2
          rounded
        "
        type="submit"
        @click="submit"
      >
        送信
      </button>
    </form>
    <ul>
      <li v-for="result in results" :key="result.id">
        id:
        <nuxt-link :to="'/posts/' + result.id">{{ result.id }}</nuxt-link>
        | name:{{ result.name }} | 本文:{{ result.body }}
        <button @click="remove(result.id)">X</button>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  async asyncData(context) {
    // const LOCAL = 'http://localhost/'
    // const PROD = 'https://laraveltestapp111.herokuapp.com/'
    const res = await context.$axios.$get(
      `https://laraveltestapp111.herokuapp.com/api/test1/`
    )
    return {
      results: res.result,
    }
  },
  data() {
    return {
      results: '',
      name: '',
      body: '',
    }
  },
  methods: {
    // laravelのPostControllerのstoreにデータを送る。
    submit() {
      // const LOCAL = 'http://localhost/'
      // const PROD = 'https://laraveltestapp111.herokuapp.com/'
      // DBへの登録が完了したら、getでDBからデータを取ってきて追加したデータを画面に表示させる。
      axios
        .post('https://laraveltestapp111.herokuapp.com/api/store', {
          name: this.name,
          body: this.body,
        })
        .then(() => {
          axios
            .get('https://laraveltestapp111.herokuapp.com/api/test1')
            .then((response) => {
              this.results = response.data.result
              console.log(this.results)
            })
        })
    },
    remove(id) {
      // const LOCAL = 'http://localhost/'
      // const PROD = 'https://laraveltestapp111.herokuapp.com/'
      axios
        .post('https://laraveltestapp111.herokuapp.com/api/delete', { id })
        .then(() => {
          axios
            .get('https://laraveltestapp111.herokuapp.com/api/test1')
            .then((response) => {
              this.results = response.data.result
            })
        })
    },
  },
}
</script>
