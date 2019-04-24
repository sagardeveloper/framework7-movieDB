<template>
	<f7-page class="backgg">
		<f7-navbar>
			<f7-nav-left>
				<f7-link back icon="icon-back" open-panel="left"></f7-link>
			</f7-nav-left>

			<f7-nav-center sliding class="headd" style="font-family: serif;">Movie Details</f7-nav-center>
		</f7-navbar>

		<f7-preloader id="load" style="width:50px; height: 50px;  margin: 50% 50% 50% 45%;  position: absolute; color:black;"></f7-preloader>

		<div style="height: 43%;">
			<h5 style="position: absolute; margin: 20% 20% 0% 37%;">Image Loading...</h5>
			<img  style="width: 100%; z-index:1; position: absolute;" :src="'https://image.tmdb.org/t/p/w500/' + posts.backdrop_path" />	

		</div>			
		<h4  class="txt">{{posts.original_title}}</h4>
		<h4 class="txt">RATTING: {{posts.vote_average}}</h4>
		<h4 class="txt">RELEASE DATE: {{posts.release_date}}</h4>
		<f7-icon style="color: black; left: 38%;"f7="share"></f7-icon>
		<f7-icon style="color: black;left: 42%;"f7="heart"></f7-icon>
		<f7-icon style="color: black;left: 45%;"f7="cloud_download"></f7-icon>
		<br>
		<p style=" text-align: justify; padding: 1% 5% 0 5%; color: black;  ">{{posts.overview}}</p>


		
	</f7-page>
</template>

<script >
	
	import Vue from 'vue';
	var myApp=new Framework7();
	import axios from 'axios';
	import API from '../../js/api.js'

	var $$=window.Dom7;
	var current;


	export default {
		data() {
			return {
				id:this.$route.params.postId,
				posts: [],
				message:""

				}
			},

	   // Fetches posts when the component is created.
	   methods: {
	   	onF7Init:function()
	   	{
	   		current=this;
	   		this.theater();
	   		
	   	},

	   	value1:function(id)
	   	{
	   		console.log(id)

	   	},

	   	theater: function()
	   	{
	   		
	   		axios.get('https://api.themoviedb.org/3/movie/'+this.id+'?api_key='+API+'&language=en-US')
	   		.then(response => {
	      // JSON responses are automatically parsed.
	      current.posts = response.data

	      $$('#load').hide();

	  })
	   	}

	   }
	}
</script>
<style type="text/css">

.txt
{
	text-align: center;
	line-height: 0px;
	color: black;
}
.headd
{
	text-align: center;
	font-size: 120%;
	color: black;
	font-family:  serif;
	
}
.backgg
{
	background-color: white;
}

</style>