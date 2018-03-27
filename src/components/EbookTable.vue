<template>
  <el-main>
    <div style="margin-top: 15px;">
      <el-input placeholder="搜尋您想比價的電子書名關鍵字" v-model="input" v-on:keyup.enter="submitSearch" class="input-with-select">
        <el-button v-on:click="submitSearch" slot="append" icon="el-icon-search"></el-button>
      </el-input>
    </div>
    <div class="box-wrapper center">
      <vue-spinner :loading="isLoading" color="#409EFF" size="45px" margin="24px"></vue-spinner>
    </div>

    <book-item v-for="(book, index) in booksCompany"
      v-bind:title="'博客來'"
      v-bind:book="book"
      :index="index"
      :key="book.id">
    </book-item>

    <book-item v-for="(book, index) in readmoo"
      v-bind:title="'Readmoo 讀墨'"
      v-bind:book="book"
      :index="index"
      :key="book.id">
    </book-item>

    <book-item v-for="(book, index) in kobo"
      v-bind:title="'Rakuten kobo'"
      v-bind:book="book"
      :index="index"
      :key="book.id">
    </book-item>

    <book-item v-for="(book, index) in taaze"
      v-bind:title="'讀冊生活 TAAZE'"
      v-bind:book="book"
      :index="index"
      :key="book.id">
    </book-item>

    <book-item v-for="(book, index) in bookWalker"
      v-bind:title="'BOOKWALKER'"
      v-bind:book="book"
      :index="index"
      :key="book.id">
    </book-item>

    <book-item v-for="(book, index) in playStore"
      v-bind:title="'Google Play'"
      v-bind:book="book"
      :index="index"
      :key="book.id">
    </book-item>

    <book-item v-for="(book, index) in playStore"
      v-bind:title="'Google Play'"
      v-bind:book="book"
      :index="index"
      :key="book.id">
    </book-item>
    
    <book-item v-for="(book, index) in pubu"
      v-bind:title="'Pubu 電子書城'"
      v-bind:book="book"
      :index="index"
      :key="book.id">
    </book-item>

  </el-main>
</template>

<script>
import PacmanLoader from 'vue-spinner/src/PacmanLoader';
import BookItem from './BookItem';

export default {
  name: 'ebook-table',
  components: {
    'vue-spinner': PacmanLoader,
    'book-item': BookItem 
  },
  data () {
    return {
      input: '',
      booksCompany: [],
      readmoo: [],
      kobo: [],
      taaze: [],
      bookWalker: [],
      playStore: [],
      pubu: [],
      isLoading: false,
    }
  },
  methods: {
    submitSearch() {
      this.isLoading = true;
      this.axios.get('https://ebook.yuer.tw/search', {
        params: {
          q: this.input
        }
      }).then((res) => {
        if(res.data){
          for(let index in res.data) {
            this[index] = res.data[index]
          }
          this.isLoading = false;
        }
      }).catch((err) => {
        if(err.msg) {
          console.log(err);
          this.isLoading = false;
        }
      });
    }
  }
}
</script>

<style lang="scss" scoped>
* body {
  font-size: 14px;
}

.box-wrapper {
  display: flex;
  padding: 16px;

  &.books {
    border-bottom: 1px solid #d2d2d2;
  }

  &.center {
    justify-content: center;
    margin-top: 42px;
  }

  .box {
    padding: 12px;
    margin: 0 8px;

    .price {
      font-size: 1.5rem;
      color: lighten(black, 20%);
      margin-left: 8px;
      padding: 0.5rem 1rem;
    }
  }
}

.search-btn {
  margin: 0 12px;
}

</style>
