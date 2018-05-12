<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>
      <a href="/views/index.html">跳转到index页</a>
    </h2>
    <router-link :to="{ name: 'testRouter' }">测试demo.html页里面的子路由</router-link>
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'demo页内容'
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
