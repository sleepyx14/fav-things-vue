<template>
  <div>
		<div id="input">
			<span id="search_txt">Seach:</span>
			<input v-model="srchVal" placeholder="Look for something!">
			<button v-on:click="srchWiki"></button>
		</div>
		<div id="results">{{res}}</div>
  </div>
</template>

<script>
export default {
	data: (){
		return {
			res: "",
		}
	}
  name: 'AppFavContainer',
	methods:{
			srchWiki: ()=>{
				let endpoint = "https://en.wikipedia.org/w/api.php?&origin=*&action=opensearch&search="+srch_val+"&limit=1&format=json"

		    /*
		    fetch, store, and display data
		    */
		    fetch(endpoint)
		      .then((response) => {
		        return response.json();
		      })
		      .then((myJson) => {
		        const title = myJson[0]
		        const description = myJson[2]
		        const link = myJson[3]

		        return {title:title, description:description, link:link}
		      })
		      .then((srch_data) => {
		        const title = srch_data.title
		        const description = srch_data.description
		        const link = srch_data.link


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
