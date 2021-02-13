<template>
  <div>
    <input type="text" v-model="keyword">
    <button @click="search(keyword)">検索する</button>
  </div>
</template>

<script>
export default {
  name: 'BookSearch',
  data() {
    return {
      keyword: '',
      searchResult: []
    }
  },
  methods: {
    async search(keyword) {
      this.searchResult = []
      const baseUrl = 'https://www.googleapis.com/books/v1/volumes?'
      const params = {
        q: `intitle:${keyword}`,
        maxResults: 40
      }
      const queryParams = new URLSearchParams(params)

      const res = await fetch(baseUrl + queryParams)
      .then(res => res.json())
      console.log(res.items)
      
      for(let book of res.items) {
        let title = book.volumeInfo.title
        let img = book.volumeInfo.imageLinks
        let description = book.volumeInfo.description

        this.searchResult.push({
          title: title ? title : '',
          image: img ? img.thumbnail : '',
          description: description ? description.slice(0, 40) : '',
        })
      }
    }
  },

}
</script>

<style>

</style>