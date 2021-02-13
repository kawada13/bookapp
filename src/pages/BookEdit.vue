<template>
  <div>
    bookedit
    {{books[$route.params.id]}}
    <v-btn
          color="secondary"
          to="/search"
          >
          検索に戻る
          </v-btn>
  </div>
</template>

<script>
export default {
  name: 'BookEdit',
  props: {
    books: Array
  },

}
</script>

<style>

</style>