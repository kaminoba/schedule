<template>
	<div id="app">
		<ul>
			<li v-for="(row, index) in itemList" v-bind:key="index">
				<label>{{ row.datetime }}：{{ row.content }}</label>
				<button @click="deleteItem(index)">Delete</button>
				<router-link :to="'/edit/${index}'">Edit</router-link>
			</li>
		</ul>
	</div>
</template>

<script>
	export default {
		data(){
			return{
				itemList:[]
			}
		},
		created(){
			this.axios.get('https://api.example.com/list')
				.then(response => {
					this.itemList = response.data;
				})
				.catch(response => console.log(response))
		},
		methods: {
			deleteItem(index){
				this.axios.delete('https://api.example.com/delete/'+index)
				.then(response => {
					console.log(response)
					this.itemList.splice(index, 1)
				})
				.catch(response => console.log(response))
			}
		}
	}
</script>