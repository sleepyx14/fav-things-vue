<template>
  <div>
		<div id="input">
			<span id="search_txt">Seach:</span>
			<input v-model="srchVal" placeholder="Look for something!">
			<button v-on:click="srchWiki"></button>
		</div>

		<div class="res">
			<span id="res_title">{{title}}</span>
			<div id="res_description">{{description}}
				<br/><a v-if="description" :href="link">More Info</a>
			</div>
		</div>
  </div>
</template>

<script>
export default {
	data(){
		return {
			srchVal: "",
			title: "",
			description: "",
			link: "",
		}
	},
  name: 'AppFavContainer',
	methods:{
			srchWiki: function (){
				let endpoint = "https://en.wikipedia.org/w/api.php?&origin=*&action=opensearch&search="+this.srchVal+"&limit=1&format=json"

				/*
				fetch, store, and display data
				*/
				fetch(endpoint)
				.then((response) => {
					return response.json();
				})
				.then((myJson) => {
					this.title = myJson[0]
					this.description = myJson[2]
					this.link = myJson[3]
				})
			}
	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
body{
  font: 1em/150% Helvetica, Arial, sans-serif;
  padding: 1em;
  margin: 0 auto;
  max-width: 33em;
  background-color: #36454f;
}

#input, #res_title{
  text-align: center;
  display: block;
  background-color: #a6a6a6;
  color: white;
  border:1px solid black;
}

#input{
  padding-top: 0.5em;
  padding-bottom: 0.5em;
}

#results{
  margin-top: 1em;
}

#res_title{
  font-size: 1.25em;
  margin-top: 0.25em;
}

#res_description{
  background-color: rgb(204, 85, 50);
  color: white;
  padding: 2em;
  border:1px solid black;
}
button {
  background-color: #36454f;
  border: none;
  padding: 15px 18px 5px 23px;
	margin-left: 1em;
	border-radius: 25px;
}

button:hover{
	background-color: #315771;
}

a{
  color:white;
}

a:visited{
  color:white;
}
</style>
