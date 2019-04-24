<template>
	<f7-page class="backg">
		<f7-navbar title="All Movies" class="head" back-link="Back" sliding>
			
		</f7-navbar>
		<div class="smallcardwapp ion-cardslidee" v-for="(post,index) in posts" :key="index">		
			<img style="width: 95%; border-radius: 3%;" :src="'http://image.tmdb.org/t/p/w500' + post.poster_path" @click="value1(post)"/> 

		</div>

	</f7-page>
</template>

<script >
	

	import axios from 'axios';
	import API from '../../js/api.js'

	var $$=window.Dom7;
	var current;
	export default {
		data() {
			return {
				posts: []


			}
		},

	   // Fetches posts when the component is created.
	   methods: {onF7Init:function()
	   	{
	   		current=this;
	   		this.theater();
	   		
	   	},

	   	value1:function(id)
	   	{
	   		console.log('fffid');
	   		console.log(id);

	   		this.$f7.mainView.router.load({
	   			url:  "/movielist/imgg/"+id.id+"/" 
	   		})	

	   	},



	   	theater: function()
	   	{
	   		
	   		
	   		axios.get('https://api.themoviedb.org/3/discover/movie?api_key='+API+'&primary_release_date.gte=2018-02-1&primary_release_date.lte=2018-02-21')
	   		.then(response => {
	      // JSON responses are automatically parsed.
	      current.posts = response.data.results

	  })
	   	}

	   }
	}
</script>


<style type="text/css">

.ion-cardslidee {

	width: 32% !important;
	height: 34%;
	display: inline-block;
	margin-left: 1.2%;
	margin-bottom: 0%;
	padding-top: 0;
	padding-bottom: 0;     
}
.smallcardwapp
{

	width:61%;
	height:30%; 
	margin-top: 0%;
	margin-bottom: 0%;
	overflow-y:hidden;
	overflow-x:hidden;
}
.head
{
	text-align: center;
	font-size: 100%;
	color: black;
	font-family:  serif;
	
}
.backg
{
	background-color: black;
	border: white;
}



</style>