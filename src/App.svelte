<script>
	import MatchCard from './MatchCard.svelte';
	import { onMount, beforeUpdate } from 'svelte';
	import { writable } from 'svelte/store';
  
	let eventCode = '';
	let isSearching = false;
  
	const matchesStore = writable([]);
  
	const fetchMatches = async () => {
	  try {
		isSearching = true;
		const response = await fetch(`https://api.statbotics.io/v2/matches/event/${eventCode}`);
		
		if (response.status === 404) {
		  throw new Error('Event not found. Please check the event code.');
		}
  
		const data = await response.json();
  

		matchesStore.set(data);

		console.log("The current message is:", $matchesStore);
  
	  } catch (error) {
		console.error('Error fetching matches:', error.message);
	  } finally {
		isSearching = false;
	  }
	};
  

	let unsubscribe;
	onMount(() => {
	  unsubscribe = matchesStore.subscribe(() => {});
	  fetchMatches();
	});
  

	beforeUpdate(() => {
	  if (unsubscribe) {
		unsubscribe();
	  }
	});
  </script>
  
  <main>
	<h1>Statbotics Event Viewer</h1>
	<input bind:value={eventCode} placeholder="Enter event code" />
	<button on:click={fetchMatches} disabled={isSearching}>
	  {#if isSearching}
		Searching...
	  {:else}
		Search
	  {/if}
	</button>
  
	{#if $matchesStore && $matchesStore.length > 0}
	  {#each $matchesStore as match (match.key)}

		<MatchCard {match} />
	  {/each}
	{:else}
	  {#if !isSearching}
		<p>No matches found.</p>
	  {/if}
	{/if}
  </main>
  
  <style>
	main {
	  text-align: center;
	  padding: 20px;
	}
  
	input, button {
	  margin: 5px;
	}
  </style>
  