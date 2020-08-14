<template>
  <div>
    <!-- template categries -->
    <v-container class="ma-0 pa-0" grid-list-sm>
      <div class="text-right">
        <v-btn small text to="/categories" class="blue--text">
          All Categories
          <v-icon>mdi-chevron-right</v-icon>
        </v-btn>
      </div>
      <v-layout wrap>
        <v-flex v-for="(category, index) in categories" :key="`category-`+category.id" xs6>
          <v-card :to="'/category/'+ category.slug">
            <v-img :src="getImage('/categories/'+category.image)" class="white--text">
              <v-card-title class="fill-height align-end" v-text="category.name">{{index}}</v-card-title>
            </v-img>
          </v-card>
        </v-flex>
      </v-layout>
    </v-container>
    <!-- template books -->
    <v-container class="ma-0 pa-0 mt-2" grid-list-sm>
      <div class="text-right">
        <v-btn small text to="/books" class="blue--text">
          All Books
          <v-icon>mdi-chevron-right</v-icon>
        </v-btn>
      </div>
      <v-layout wrap>
        <v-flex v-for="(book, index) in books" :key="`book-`+book.id" xs6>
          <v-card :to="'/book/'+ book.slug">
            <v-img :src="getImage('/books/'+book.cover)" class="white--text">
              <v-card-title class="fill-height align-end" v-text="book.title">{{index}}</v-card-title>
            </v-img>
          </v-card>
        </v-flex>
      </v-layout>
    </v-container>
  </div>
</template>

<script>
export default {
  name: "Home",
  components: {},
  data: () => ({
    categories: [],
    books: [],
  }),
  created() {
    console.log("get data random categories");
    this.axios
      .get("/categories/random/2")
      .then((response) => {
        let { data } = response.data;
        this.categories = data;

        // console.log(data);
      })
      .catch((error) => {
        let { response } = error;
        console.log(response);
      });
    console.log("get data top books");
    this.axios
      .get("/books/top/4")
      .then((response) => {
        let { data } = response.data;
        this.books = data;

        // console.log(data);
      })
      .catch((error) => {
        let { response } = error;
        console.log(response);
      });
  },
  methods: {},
};
</script>
