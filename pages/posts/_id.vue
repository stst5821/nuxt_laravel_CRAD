<template>
  <div>
    id:{{ result_id }} | name:{{ result_name }} | 本文:{{ result_body }}

    <form @submit.prevent>
      <input
        v-model="result_id"
        placeholder="入力ください"
        type="hidden"
        name="entry"
        @keyup.enter="submit"
      />
      <br />
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
  </div>
</template>

<script>
import axios from 'axios'

export default {
  async asyncData(context) {
    const res = await context.$axios.$get(
      `http://localhost/api/edit/${context.params.id}`
    )
    console.log(res)
    return {
      result_id: res.result.id,
      result_name: res.result.name,
      result_body: res.result.body,
    }
  },
  data() {
    return {
      results: '',
      id: '',
      name: '',
      body: '',
    }
  },
  methods: {
    // laravelのPostControllerのstoreにデータを送る。
    submit() {
      const CORS_PROXY = 'http://localhost/'
      // DBへの登録が完了したら、getでDBからデータを取ってきて追加したデータを画面に表示させる。
      axios.post(CORS_PROXY + 'api/update', {
        id: this.result_id,
        name: this.name,
        body: this.body,
      })
    },
  },
}
</script>
