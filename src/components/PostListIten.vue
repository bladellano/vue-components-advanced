<template>
  <div class="post">

    <slot>

      <div class="post-header">
        <h2> {{ post.title }}</h2>
      </div>

      <div class="post-content">
        <p> {{ post.content }} </p>
      </div>
      
      <div class="post-footer">
        <small> {{ post.author }} </small>
        <a href="#" class="link">Ler mais...</a>
      </div>

    </slot>

  </div>
</template>

<script>

export default{
  props:{
    post:{
      type:Object,
      required: true
    }
  }
}

</script>

<style scoped>
.post {
  margin: 15px auto;
}
.post-header {
  padding: 5px 12px;
  background-color: #069;
  color: #fff;
}
.post-content {
  font-size: 16px;
}
.post-footer {
  font-style: italic;
}
.link{
    color: #069;
    float: right;
}
</style>