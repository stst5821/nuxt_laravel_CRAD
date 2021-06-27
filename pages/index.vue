<template>
  <div>
    {{ data }}
    {{ data }}
  </div>
</template>

<script>
export default {
  async asyncData({ app }) {
    const data = await app.$axios.$get(`/api`)
    return { data }
  },
}
</script>
