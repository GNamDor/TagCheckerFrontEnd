<script lang="ts">
	// import welcomeFallback from '$lib/images/svelte-welcome.png';
	import { PostTags } from '../lib/api.config.js'; 
	import { fade } from 'svelte/transition';

	let newText = '';
	// let results = [];
	let results = "";
	let errorMessage = '';

	async function handlePostTag() {
		try {
			const res = await PostTags(newText);
				// results = [...results, res];
				results = res
				newText = '';
				errorMessage = '';
			} catch (error) {
				errorMessage = error.message;
				console.error('Error creating todo:', error);
			}
	}
	$: hasResults = results && results.length > 0;
</script>

<svelte:head>
	<title>Tag Checker</title>
	<meta name="description" content="Tag Checker frontend made in svelte" />
</svelte:head>


<section class="parent-container">

	<div class="top-div">
		<h1>
			Tag Checker<br />
		</h1>

		<h2>
			please enter <strong>some text below</strong> to see if the tags are properly closed
		</h2>

		<input class= "text-field" bind:value={newText} type="text" id="fname" name="fname"><br><br>
		<input on:click={handlePostTag} type="submit" value="Submit">
	</div>
	<div class="bottom-div">
		{#if hasResults}

			<h1 transition:fade={{ duration: 500 }}>
				<pre>{results}</pre>
			</h1>
		{/if}
	</div>
	
</section>

<style>

	.parent-container {
		/* display: flex;
		flex-direction: column;
		justify-content: center; 
		align-items: center;    */
		height: 100vh;        
	}

	.top-div{
			height: auto;
			padding-top: 10%;

		}

	.bottom-div{
		padding-top: 0px;
	}

	div {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}

	h1 {
		width: 100%;
	}

	input[type=text] {
		padding: 10px;
		border: 1px solid #ccc;
		border-radius: 4px;
		box-sizing: border-box;
		margin-bottom: 10px;
		font-family: sans-serif; /* A clean, modern font */
		font-size: 16px;
		color: #333; /* Dark gray for text */
	}

	.text-field {
		max-height: 200px;
		height: 0.5vh;
		min-height: 70px;
		width: 100%;
	}

	input[type=submit] {
		background-color: #444; /* Dark gray background */
		color: white;
		padding: 10px 15px;
		border: none;
		border-radius: 4px;
		cursor: pointer;
		font-family: sans-serif;
		font-size: 16px;
		transition: background-color 0.3s ease; /* Smooth hover effect */
	}

	input[type=submit]:hover {
		background-color: #666; /* Slightly lighter gray on hover */
	}

	h1 {
		font-size: 2.5em; /* Slightly larger than default */
		color: #333; /* A dark gray for monotone */
		font-family: sans-serif; /* Modern font */
		}

	h2 {
		font-size: 2em; /* Larger than default, smaller than h1 */
		color: #555; /* A lighter shade of gray for hierarchy */
		font-family: sans-serif;
		}
	
</style>
