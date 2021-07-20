<script context="module">
	import Client from '$lib/client'
	import  * as PrismicHelpers from "@prismicio/helpers";
	
	export async function load({fetch})  {
	  const document = await Client(fetch).getByUID('blog_homepage','my-page', {'fetchLinks': 'author.author_name'});
		console.log("document is",document)
		if(document){
		  return {
			props: {
			  document
			}
		  };
		} else {
		   return {
			 status: 404,
			 error: "Post not found",
			};
		  }
	  }
  </script>
  
  <script>
	export let document;
  </script>
  
  <main>
	<div class="container">
	  {PrismicHelpers.asDate(document.data.date)}
	  { @html PrismicHelpers.asHTML(document.data.main_title)}
	  { @html PrismicHelpers.asHTML(document.data.rich_text)}
	  { PrismicHelpers.asText (document.data.rich_text)}
	  { PrismicHelpers.asDate(document.data.timestamp)}
	  <a href={PrismicHelpers.asLink(document.data.link_to_web)}>Example Link</a>


	</div>
  </main>
  
  <style>
	main {
	  font-family: sans-serif;
	}
	.container {
	  display: flex;
	  flex-direction: column;
	  align-items: center;
	  padding: 0px 20px;
	}
	.container > * {
	  width: 100%;
	  max-width: 700px;
	}
  </style>
  