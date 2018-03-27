<template>
  <div class="box-wrapper books">

    <div class="box img flex-1">
      <img :src="book.thumbnail" :alt="book.title" class="image">
    </div>

    <div class="box flex-2">
      <h4>
        <a :href="book.link">{{ book.title }}</a>
      </h4>
      <el-tag type="success">{{ title }}</el-tag>
      <span class="price">{{ book.price }} {{ book.priceCurrency }}</span>
    </div>

    <div class="box flex-3">
      <h2>介紹</h2>
      <p>{{ book.about }}</p>
    </div>

  </div>
</template>


<script>
  export default {
    name: 'book-item',
    props: ['title', 'book']
  };

</script>

<style lang="scss" scoped>
* body {
  font-size: 14px;
}

a {
  color: #2B81DA;
  text-decoration: none;
}

h2 {
  color: lighten(black, 20%);
}

p {
  color: lighten(black, 35%);
}

.image {
  width: 100%;
  display: block;
  flex: left;
  border-radius: 5px;
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

.flex-1 {
  flex: 1;
}

.flex-2 {
  flex: 2;
}

.flex-3 {
  flex: 3;
}

.flex-8 {
  flex: 8;
}


</style>