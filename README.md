# nuxt-lara-app

vercel へのデプロイ

setting の build command で、override のトグルをオンにして
$ nuxt generate
と入力。

そのほかはそのままで OK。

pages.index.vue の記述を以下のようにする。

```
<script>
export default {
  async asyncData({ app }) {
    const data = await app.$axios.$get(
      `https://laraveltestapp111.herokuapp.com/api` // ←herokuに上げたLaravelのURL + /api と書く。
    )
    return { data }
  },
}
</script>
```

ここの URL を間違えると、networkerror というエラー画面になる。

開発環境か本番環境かで api のアクセス先を自動で変更する。

cross-env インストール
npm install --save cross-env
