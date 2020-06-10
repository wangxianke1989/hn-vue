<template>
	<div class ='bar'>
		<h2>Hacker News</h2>
		<form>
		<input
			type="text"
			class="input"
			:value="value"
			v-on="listeners"
		>
		<button type="submit">Search</button>
		</form>
	</div>
</template>

<script>
export default{
	props:{
		value:{
			type:String,
			default:''
		}
	},
	computed:{
		listeners(){
			return{
				...this.$listeners,
				input:event=>this.$emit('input',event.target.value)
			}
		}
	}
}
</script>
<style>
.bar{
	display: flex;
	background-color:#F84E1D;
	justify-content:space-around;
	//border:solid blue;
}
h2{
	//border:solid yellow;
	margin-left:60px;
}
form{
	display:flex;
	align-self:center;
	//border:solid yellow;
	flex-grow:1;
	margin:0 60px 0 40px;
	height:35px;

}
input{
	flex-grow:1;
}
</style>