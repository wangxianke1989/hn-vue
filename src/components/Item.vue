<template>
	<div class="post">
	<li >
		<div class="title-url">
			<div class="title">{{post.title}}</div>
			(<div class="url"><a v-bind:href="post.url">{{post.url}}</a></div>)
		</div>
		<div class ="reference">{{post.author}}|{{post.created_at_i}}  |{{post.num_comments}} comments</div>
	</li>
	</div>
</template>

<script>
export default{
	props:['post']
}

</script>

<style>
.post{
	//border:solid green;
	display:flex;
	flex-direction:column;
	list-style:none;
	margin:0 0 7px 0;

}

.title-url{
	display:flex;
	flex-wrap:wrap;

}
.url{

	font-size:8px;

}
a{
	text-decoration:none;
	color:#848383;
}
.title{
	font-size:15px;
	font-weight:500;
}
.reference{
	display:flex;
	font-size:5px;
	font-weight:lighter;
	color:#848383;
}
</style>