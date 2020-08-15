<template>
	<div id="app">
		<div>
			<span>Datetime:</span><input type="text" v-model="editDatetime">
			<span>Content:</span><input type="text" v-model="editContent">
			<button v-on:click="editItem()">Edit Schedule</button>
		</div>
	</div>
</template>

<script>
	export default {
		data(){
			return{
				editDatetime: "",
				editContent: ""
			}
		},
		created(){
			this.axios.get('https://api.example.com/detail/'+this.$route.params.id)
				.then(response => {
					this.editDatetime = response.data.datetime
					this.editContent = response.data.content;
				})
				.catch(response => console.log(response))
		},
		methods: {
			editItem(){
				if(this.editDatetime=="" || this.editContent==""){
					alert("Please input value");
					return;
				}
				this.axios.patch('https://api.example.com/edit/'+this.$route.params.id,{
					datetime: this.editDatetime,
					content: this.editContent
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