<template>
	<div id="app">
		<ul>
			<li v-for="(row, index) in itemList" v-bind:key="index">
				<label>{{ row.datetime }}：{{ row.content }}</label>
				<button @click="deleteItem(index)">Delete</button>
			</li>
		</ul>
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
				itemList:[],
				newDatetime: "",
				newContent: ""
			}
		},
		methods:{
			addItem(){
				if(this.newDatetime=="" || this.newContent==""){
					alert("Please input value");
					return;
				}
				this.itemList.push({
					datetime: this.newDatetime,
					content: this.newContent
				});
				this.newDatetime = "";
				this.newContent = "";
			},
			deleteItem(index){
				this.itemList.splice(index, 1)
			}
		}
	}
</script>