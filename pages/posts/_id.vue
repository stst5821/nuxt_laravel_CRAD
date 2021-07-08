<template>
  <div>
    <div v-for="result in results" :key="result.id">
      id:{{ result.id }} | name:{{ result.name }} | 本文:{{ result.body }}
    </div>
  </div>
</template>

<script>
export default {
  async asyncData(context) {
    const res = await context.$axios.$get(
      `http://localhost/api/edit/${context.params.id}`
    )
    console.log(res)
    return {
      results: res,
    }
  },
  data() {
    return {
      results: '',
      name: '',
      body: '',
    }
  },
}
</script>
