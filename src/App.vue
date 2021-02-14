<template>
  <v-app>
    <Header />
    <v-main>

      <v-container>
       <router-view 
       @add-book-list="addbook"
       @update-book-info="updateBookInfo"
       :books="books"
       />
      </v-container>
    </v-main>
    <Footer />
  </v-app>
</template>

<script>
import Header from '@/global/Header.vue';
import Footer from '@/global/Footer.vue';

export default {
  name: 'App',

  components: {
    Header,
    Footer
  },

  data() {
    return {
      books: [],
      newbook: null,
    }
  },
  created() {
    if (localStorage.getItem('books')) {
      try {
        this.books = JSON.parse(localStorage.getItem('books'));
      } catch(e) {
        localStorage.removeItem('books');
      }
    }
  },
  methods: {
    addbook(e) {

      this.books.push({
        id: this.books.length,
        title: e.title,
        image: e.image,
        description: e.description,
        readDate: '',
        memo: ''
      });
      // this.newbook = '';
      this.savebooks();
      // console.log(this.books.slice(-1)[0].id);
      this.goToEditPage(this.books.slice(-1)[0].id)
    },
    removebook(x) {
      this.books.splice(x, 1);
      this.savebooks();
    },
    savebooks() {
      const parsed = JSON.stringify(this.books);
      localStorage.setItem('books', parsed);
    },
    updateBookInfo(e) {
      const updateInfo = {
        id: e.id,
        title: this.books[e.id].title,
        image: this.books[e.id].image,
        description: this.books[e.id].description,
        memo: e.memo,
        readDate: e.readDate
      }

      this.books.splice(e.id, 1, updateInfo)

      this.savebooks()
      this.$router.push('/')
    },
    goToEditPage(index) {
      this.$router.push({ name: 'BookEdit', params: { id: index } })
    }
  }

};
</script>
