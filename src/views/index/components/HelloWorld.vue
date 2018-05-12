<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>
      <a href="/views/demo.html">跳转到demo页</a>
    </h2>
    <router-link :to="{ name: 'testRouter' }">index.html中的子路由</router-link>
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: '首页内容'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
