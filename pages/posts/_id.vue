<template>
  <div>
    id:{{ result_id }} | name:{{ result_name }} | 本文:{{ result_body }}
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
      result_id: res.result.id,
      result_name: res.result.name,
      result_body: res.result.body,
    }
  },
}
</script>
