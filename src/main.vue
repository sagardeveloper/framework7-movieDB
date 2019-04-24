<template>
	<!-- App -->
	<div id="app">

		<!-- Main Views -->
		<f7-views >
			
			<f7-view id="main-view" navbar-through :dynamic-navbar="true" main>

				<!-- Navbar -->
				<f7-navbar >
					<div  class="box"   style="width: 100%;background-color: white; height: 100%; left: 0px;">
						<input  style="width:100%;padding-left: 2%; background-color: white; height: 89%;" v-model="messagee" placeholder="Search movie" v-on:keyup="valuu()">
					</div>

					<!-- F7 Icons font icon -->
					
					<f7-nav-center>
						<img  style="width: 8%; padding-left:0%;" src="./assets/images/gaana.png"/>
						<!-- 	-->
						<div style="margin-left: 31.5%; " class="head"> Movie Cloud </div>
					</f7-nav-center>
					<f7-nav-left>
						<div  class="search" @click="search()"> <f7-icon style="font-size: 100%;"  f7="search"  ></f7-icon>
							<!-- Popover content goes here -->
						</div>
					</f7-nav-left>
				</f7-navbar>
				<div style="overflow: scroll;">
					<f7-list media-list id="mylist" swipeout:open >

						<f7-list-item  v-for="(api,index) in searchapi" :key="index"  @click="value11(api)" >
						{{api.original_title}}</f7-list-item>

					</f7-list>
				</div>
				<!-- Pages -->
				<f7-pages >
					
					<f7-page class="backg" >
						<div @click="mainbox()" style="height: 100%;">

							<!-- Main swiper -->
							<f7-swiper class="swipe" id="banner-swiper" 
							:params="{ observer: true}">

							<f7-swiper-slide v-for="(post,index) in posts" :key="index" http-equiv="refresh"  >				
								<h5 class="imagetitle">{{post.original_title}}</h5>
								<img style=" max-width: 100%" :src="'https://image.tmdb.org/t/p/w500' + post.backdrop_path" @click="value1(post)"/>
							</f7-swiper-slide>
						</f7-swiper>
						<!-- first row -->
						<div class="smallcardwap" style="padding-top: 0%;">

							<f7-button  href="/details/" style=" width:  27%;font-size: 80%; float: right; position: absolute; margin-left: 72%; margin-top: 4%;  color: white">
								SEE MORE
							</f7-button>

							<h4 style="margin-left: 3%; color: white;" class="heading">TOP RATED MOVIES</h4>

							<f7-swiper :params="{ observer: true}" style="max-width: 100%;">
								<f7-swiper-slide data-space-between="10" v-for="(post,index) in posts1" :key="index" class="ion-cardslide col-33">
									<div style="max-height: 26vh;">
										<img style="max-width: 100%; border-radius: 3%;" :src="'http://image.tmdb.org/t/p/w500' + post.poster_path" @click="value1(post)"/> 
									</div>
								</f7-swiper-slide>
							</f7-swiper>
						</div>

						<!-- second row -->
						<div class="smallcardwap" style="padding-top: 0%;">

							<f7-button  href="/details/" style=" width:  27%;font-size: 80%; float: right; position: absolute; margin-left: 72%; margin-top: 4%;  color: white">
								SEE MORE
							</f7-button>

							<h4 style="margin-left: 3%; color: white;" class="heading">NEW RELEASED MOVIES</h4>

							<f7-swiper :params="{ observer: true}">
								<f7-swiper-slide v-for="(post,index) in posts2" :key="index" class="ion-cardslide" >
									<div style="max-height: 26vh;">
										<img style="width: 100%; border-radius: 3%;" :src="'http://image.tmdb.org/t/p/w500' + post.poster_path" @click="value1(post)"/> 
									</div>
								</f7-swiper-slide>
							</f7-swiper>
						</div>

						<!-- third row -->
						<div class="smallcardwap">

							<f7-button  href="/details/" style=" width:  27%;  font-size: 80%; float: right; position: absolute; margin-left: 72%; margin-top: 4%;  color: white">
								SEE MORE
							</f7-button>

							<h4 style="margin-left: 3%;color: white;" class="heading">POPULAR MOVIES</h4>

							<f7-swiper :params="{ observer: true}">
								<f7-swiper-slide v-for="(post,index) in posts3" :key="index" class="ion-cardslide" >
									<div style="max-height: 26vh;">

										<img  style="width: 100%; border-radius: 3%;" :src="'http://image.tmdb.org/t/p/w500' + post.poster_path" @click="value1(post)"/> 
									</div>
								</f7-swiper-slide>
							</f7-swiper>
						</div>
						<br>
					</div>
				</f7-page>	
			</f7-pages>
		</f7-view>
	</f7-views>
</div>
</template>

<script >
	import Routes from './routes.js'
	import Vue from 'vue';
	import axios from 'axios';
	import Popover  from 'vue-js-popover';
	import Swiper from 'swiper';
	import API from 'assets/js/api.js';
	Vue.use(Popover);
	var myApp=new Framework7();
	const app=new Vue();
	const MYapp=new Swiper();
	var $$=window.Dom7;
	var current;
	var inputVal;
	export default {
		data() {
			return {
				posts: [],
				posts1: [],
				posts2: [],
				posts3: [],
				imagee:[],
				name: '',
				messagee:"",
				searchapi:[]
				
			}
		},
		/* Fetches posts when the component is created.*/
		methods: {
			onF7Init:function()
			{
				current=this;
				this.theater();
				this.newrelease();
				this.toprated();
				this.english();
				$$('#mylist').hide();
				$$('.box').hide();
				$$('.search').on('click', function (e){
					$$('.box').show();
					$$(window).trigger('resize');
				});
			},
			handler:function(arg1,arg2){
				this.value1(arg1);
				this.hidden(arg2);
			},
			hidden:function()
			{
				$$('#mylist').hide();
				$$('.box').hide();
			},
			valuu:function()
			{
				"'http://image.tmdb.org/t/p/w500' + post.poster_path"
				axios.get('https://api.themoviedb.org/3/search/movie?api_key='+API+'&language=en-US&query='+this.messagee+'&page=1&include_adult=false')
				.then(response => {
					/*JSON responses are automatically parsed.*/
					current.searchapi = response.data.results;
					$$('#mylist').show();
				});
				console.log("default");
				console.log("default");
				console.log(this.messagee);
				console.log(this.searchapi);
			},
			mainbox:function()
			{
				console.log("i am mainbox")
				$$('.box').hide();
				$$('#mylist').hide();
				$$(window).trigger('resize')
			},
			search: function()
			{
				console.log("search funstion");
			},
			value1:function(id)
			{
				console.log('fffid');
				this.$f7.mainView.router.load({
					url:  "/movielist/imgg/"+id.id+"/" 
				})	
			},
			value11:function(id)
			{
				$$('#mylist').hide();
				$$('.box').hide();
				this.$f7.mainView.router.load({
					url:  "/movielist/imgg/"+id.id+"/"
				});	
			},
			searchmovie:function()
			{
				axios.get('https://api.themoviedb.org/3/search/movie?api_key='+API+'&language=en-US&query='+this.messagee+'&page=1&include_adult=false')
				.then(response => {
					/*JSON responses are automatically parsed.*/
					current.searchapi = response.data.results;
					console.log(this.searchapi)
					console.log("searchAPI")
				});
			},
			theater: function()
			{
				$$('#banner-swiper').show(); 		 
				console.log("searchbar value")  
				axios.get('https://api.themoviedb.org/3/discover/movie?api_key='+API+'&primary_release_date.gte=2018-02-1&primary_release_date.lte=2018-02-21')
				.then(response => {
					/*JSON responses are automatically parsed.*/
					current.posts = response.data.results;
					current.imagee = current.posts;
					this.posts.push();
					$$('#load').hide();
				});
			},
			newrelease: function()
			{
				axios.get('https://api.themoviedb.org/3/movie/top_rated?api_key='+API+'&language=en-US')
				.then(response => {
					/* JSON responses are automatically parsed.*/
					current.posts1 = response.data.results
					console.log(this.posts1)
					$$(this).find('.smallcardwap')[0].swiper.update()
					console.log("running")
				})
			},
			toprated: function()
			{
				axios.get('https://api.themoviedb.org/3/discover/movie?api_key='+API+'&primary_release_year=2018&sort_by=vote_average.desc')
				.then(response => {
					/* JSON responses are automatically parsed.*/
					current.posts2 = response.data.results
					console.log(this.posts2)
					console.log("running")
				})
			},
			english: function()
			{
				axios.get('https://api.themoviedb.org/3/movie/popular?api_key='+API+'&language=en-US&page=1')
				.then(response => {
					/*JSON responses are automatically parsed.*/
					current.posts3 = response.data.results
					console.log(this.posts3)
					console.log("running")
				})
			}
		}
	}	
</script>
<style type="text/css">
.swipe
{
	height: 36%;
	width: 94%;
	margin: 3% 5% 0% 3%;
	overflow: auto;
}
.ion-cardslide {
	width: 29% !important;
	height: 20%;
	display: inline-block;
	margin-left:2%;
	margin-bottom: 0%;
	padding-top: 0;
	padding-bottom: 0;  
}
.smallcardwap
{
	width:100%;
	height:40%; 
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
.imagetitle
{
	position: absolute;
	z-index: 1;
	color: white;
	font-size: 90%;
	text-align: center;
	margin: 35% 0% 0% 36.5%;
	text-shadow: 1px 1px #ff2229;
}
.search
{
	
}
.box
{
	position: absolute;
	z-index: 1;
}
#mylist
{
	position: absolute;
	z-index: 1;
}
</style>