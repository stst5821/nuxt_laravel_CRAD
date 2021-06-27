<template>
  <div>
    {{ data }}
  </div>
</template>

<script>
export default {
  async asyncData({ app }) {
    const data = await app.$axios.$get(`/api`)
    return { data }
  },
  mounted() {
    // eslint-disable-next-line no-console
    console.log(process.env.NODE_ENV)
  },
}
</script>
