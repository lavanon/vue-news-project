<script>
  import NavBar from './components/NavBar.vue';
  import NewsArticle from './components/NewsArticle.vue';

  export default {
    name: 'app',
    components: {
      NavBar,
      NewsArticle,
    },
    data() {
      return {
        search: 'tesla',
        apiData: [],
        selected: 30,
      };
    },
    mounted() {
      fetch(
        `https://api.parsely.com/v2/search?apikey=arstechnica.com&q=${this.search}&days=30`
      )
        .then((res) => res.json())
        .then((data) => (this.apiData = data.data));
    },
    methods: {
      activateSearch() {
        fetch(
          `https://api.parsely.com/v2/search?apikey=arstechnica.com&q=${this.search.replace(
            /[^\w\s]/gi,
            ''
          )}&days=${this.selected}`
        )
          .then((res) => res.json())
          .then((data) => (this.apiData = data.data));
      },
    },
  };
</script>

<template>
  <NavBar />
  <h3 class="ui headers">Search for Articles</h3>
  <div id="searchButton" class="ui fluid action input">
    <input
      type="text"
      v-on:keyup.enter="activateSearch"
      v-model="search"
      placeholder="Search..."
    />
    <div @click="activateSearch" class="ui button">Search</div>
    <select class="dropdown" v-model="selected" @change="activateSearch">
      <option disabled value="">Adjust time span</option>
      <option value="1">Today</option>
      <option value="7">This Week</option>
      <option value="30">This Month</option>
      <option value="365">This Year</option>
    </select>
  </div>
  <h3 class="ui headers margin-bottom">Search Results</h3>
  <NewsArticle
    v-for="(post, index) in apiData"
    v-bind:key="index"
    v-bind:post="post"
  ></NewsArticle>
</template>

<style>
.headers {
  margin-bottom: 0;
  padding-left: 20px;
}
#searchButton {
  padding: 20px;
}
.dropdown {
  border: 1px solid lightgray;
  margin-left: 10px;
}
.headerMargin {
  margin-top: 10px;
}
.margin-bottom {
  margin-bottom: 20px;
}
</style>
