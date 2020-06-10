<template>
  <div id="app">
    <Bar
      v-model="query"
      placeholder="Search stories by title,url or author"
      @keydown.enter="queryNews"
    />

    <div class='main'>
      <div class="filter">
      <span>Search</span>
      <select v-model='type'>
        <option>all</option>
        <option>story</option>
        <option>comment</option>
      </select>
      <span>by</span>
      <select v-model='sort'>
        <option>Date</option>
        <option>Popularity</option>
      </select>
      <span>for</span>
      <select v-model='dateRange'>
        <option>All time</option>
        <option>Last 24h</option>
        <option>Past Week</option>
        <option>Past Month</option>
        <option>Past Year</option>
        <option>Custom range</option>
      </select>
      </div>

      <ul>
        <Item
          v-for= "post in posts"
          :key = "post.objectID"
          :post = "post"
        />
      </ul>

    </div>

    <Footer/>
  </div>
</template>

<script>
import Bar from './components/Bar.vue'
import Item from './components/Item.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    Bar,
    Item,
    Footer
  },
  data(){
    return {
      query:'',
      type:'',
      sort:'',
      dateRange:'',
      posts:[]
    }
  },

  created(){
    this.getNews()
  },
  watch:{
    type:function () {
      this.queryNews()
    }
  },
  methods:{
    queryNews:function(query,type){
      let url = `http://hn.algolia.com/api/v1/search?query=${query}&tags=${type}`
      fetch(url)
      .then(res=>res.json())
      .then(data=>this.posts=data.hits)
    },
    getNews:function(){
      fetch('http://hn.algolia.com/api/v1/search?query=&tags=story')
      .then(res=>res.json())
      .then(data=>this.posts=data.hits)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0 100px 0px 100px;
  //border:solid black;
}
.main{
  display:flex;
  flex-direction:column;
  background-color:#E9E7E7;
  //border:solid blue;
}
.filter{
  margin-top:10px;

}
ul{
  display:flex;
  flex-direction:column;
  justify-content:flex-start;
  //border:solid red;
}
</style>
