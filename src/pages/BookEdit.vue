<template>
  <div>
    <v-row>
      <v-col cols="12">
        <v-card class="mx-auto">
          <v-row>
            <v-col cols="4">
              <v-img :src="book.image"></v-img>
            </v-col>
            <v-col cols="8">
              <v-card-title>
                タイトル：{{book.title}}
              </v-card-title>
              読んだ日：
              <v-menu
                v-model="menu"
                :close-on-content-click="false"
                :nudge-right="40"
                transition="scale-transition"
                offset-y
                min-width="auto"
              >
                <template v-slot:activator="{ on, attrs }">
                  <v-text-field
                    v-model="book.readDate"
                    readonly
                    v-bind="attrs"
                    v-on="on"
                  ></v-text-field>
                </template>
                <v-date-picker
                  v-model="book.readDate"
                  @input="menu = false"
                  locale="jp-ja"
                  :day-format="date => new Date(date).getDate()"
                ></v-date-picker>
              </v-menu>
              感想：
              <v-textarea
              class="mx-2"
              v-model="book.memo"
              >
              {{book.memo}}
              </v-textarea>
              <v-card-actions>
                <v-btn color="secondary" to="/">一覧に戻る</v-btn>
                <v-btn color="info" @click="updateBookInfo">保存する</v-btn>
              </v-card-actions>
            </v-col>
          </v-row>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  name: 'BookEdit',
  props: {
    books: Array
  },
  data() {
    return {
      book: '',
      date: new Date().toISOString().substr(0, 10),
      menu: false,
    }
  },
  created() {
    this.book = this.books[this.$route.params.id]
  },
  methods: {
    updateBookInfo() {
      this.$emit('update-book-info', {
        id: this.$route.params.id,
        readDate: this.book.readDate,
        memo: this.book.memo
      })
    }
  },

}
</script>

<style>

</style>