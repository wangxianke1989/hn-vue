<template >
	<div class='main'>
		<span>Search</span>
		<select v-model='type'>
			<option>All</option>
			<option>Stories</option>
			<option>Comments</option>
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
		<div class="newList">
		<ul  >
			<Item
				v-for= "post in posts"
				:key = "post.objectID"
				:post = "post"
			/>
		</ul>
		</div>
	</div>
</template>

<script>

import Item from './Item.vue'

export default{
	components:{
		Item
	},
	data(){
		return{
			posts:[],
			type:'',
			sort:'',
			dateRange:''
		}
	},
	created(){
		this.getNews()
	},
	methods:{
		getNews:function(){
			fetch('https://hn.algolia.com/api/v1/search_by_date?tags=story')
			.then(res=>res.json())
			.then(data=>this.posts=data.hits)
		}
	}
}

</script>
<style>
.main{
	display:flex;
	background-color:#DBD6D6;
	border:solid blue;
}
.newList{
	display:flex;
	flex-direction:column;
	flex-wrap:wrap;
}

</style>