<template>
	<div id="app">
		<div>
			<span>Datetime:</span><input type="text" v-model="newDatetime">
			<span>Content:</span><input type="text" v-model="newContent">
			<button v-on:click="addItem()">Add Schedule</button>
		</div>
	</div>
</template>

<script>
	export default {
		data(){
			return{
				newDatetime: "",
				newContent: ""
			}
		},
		methods: {
			addItem(){
				if(this.newDatetime=="" || this.newContent==""){
					alert("Please input value");
					return;
				}
				this.axios.post('https://api.example.com/create',{
					datetime: this.newDatetime,
					content: this.newContent
				})
				.then(response => {
					console.log(response)
					this.$router.push({ name: 'home'})
				})
				.catch(response => console.log(response))
			}
		}
	}
</script>