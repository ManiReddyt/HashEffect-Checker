<svelte:head>
	<title>SSS</title>
	<meta name="SSS Page" content="SSS Page" />
</svelte:head>

<script>
	import { onMount } from 'svelte';

/**
   * @type {null}
   */
let data = null;

let error = null;

onMount(() => {
  fetch('https://hash-effect.onrender.com/sss/shares') // Replace with your API endpoint
	.then(response => {
	  if (!response.ok) {
		throw new Error('Network response was not ok');
	  }
	  return response.json();
	})
	.then(jsonData => {
	  data = jsonData;
	  console.log("data", data)
	})
	.catch(err => {
	  error = err.message;
	});
});
</script>

<section>
	<div class="w-fit mx-auto">
		<h1 class="mx-auto text-4xl font-bold ">
		  Welcome to <span class="text-blue-500">HashEffect Test Tool</span> 
		</h1>
	  </div>
	<div class="w-full flex flex-col justify-center">
		<h1 class="font-medium text-blue-500">SSS PAYLOAD</h1>
		<div>
			<label for="name">Secret</label>
			<input
			class="border-2 border-gray-300"
			  type="text"
			  id="secret"
			  name="secret"
			  value=""
			/>
		</div>
		<div>
			{#if data}
			<h1> hi </h1>
			{/if}
		</div>
	</div>
</section>
