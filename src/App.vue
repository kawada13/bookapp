<template>
  <v-app>
    <Header />
    <v-main>
      <v-container>
       <router-view 
       @add-book-list="addbook"
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
      newbook: null
    }
  },
  mounted() {
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
    },
    removebook(x) {
      this.books.splice(x, 1);
      this.savebooks();
    },
    savebooks() {
      const parsed = JSON.stringify(this.books);
      localStorage.setItem('books', parsed);
    }
  }

};
</script>
