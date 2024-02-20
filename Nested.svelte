
<script>
		import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();
	
	let classes = "button is-link";
	let text = "Do"
	let lastState = NaN;
	export let promiseFunc; 

	function handleMessage(event) {
		dispatch(event);
	}
	
	function _doStuff() {
		text = "Doing";
		lastState = NaN;
		promiseFunc()
		.then(() => {
			lastState = 1;
			dispatch("success");
		})
		.catch((e) => {
			lastState = 0;
			dispatch("failure");
		})
		.then(() => new Promise((res) => {
			setTimeout(res, 2000);
		}))
		.finally(() => {
			lastState = NaN;
			text = "Do";
		})
	}
</script>


<button class={classes} on:click={_doStuff}>
	{#if !isNaN(lastState)}
		{#if  lastState === 1}
			 <i class="fa-solid fa-check"></i>
		{:else if lastState === 0}
			<i class="fa-solid fa-x"></i>
		{/if}
		&nbsp;
	{/if}
	{text}
</button>
