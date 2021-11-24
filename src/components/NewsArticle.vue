<script>
export default {
  name: 'news-article',
  props: {
    post: Object,
  },
};
</script>

<template>
  <div id="article">
    <a style="vertical-align: top; display: table-cell">
      <img id="img" :src="post.image_url" />
    </a>
    <div style="vertical-align: top; display: table-cell">
      <div class="ui label">{{ post.section }}</div>
      <h4 class="headerMargin">
        <a :href="post.url" target="blank" class="author">{{ post.title }}</a>
      </h4>
      <div class="text">
        <strong> By {{ post.author }} </strong> |
        {{ post.pub_date.split('T')[0] }}
      </div>
    </div>
  </div>
  <hr class="hrPadding" />
</template>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#img {
  height: 100px;
  width: 140px;
  margin-right: 20px;
  object-fit: cover;
}
.hrPadding {
  margin: 20px 0;
}
#article {
  padding-left: 20px;
  max-width: 750px;
}
</style>
