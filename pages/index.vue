<template>
  <div>
    {{ data }}
    {{ data }}
  </div>
</template>

<script>
export default {
  async asyncData({ app }) {
    const data = await app.$axios.$get(
      `https://laraveltestapp111.herokuapp.com/api`
    )
    return { data }
  },
}
</script>
