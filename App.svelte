<svelte:head>
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@0.9.4/css/bulma.min.css">
	<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css" integrity="sha512-DTOQO9RWCH3ppGqcWaEA1BIZOC6xxalwEsw9c2QQeAIftl+Vegovlnee1c9QX4TctnWMn13TZye+giMm8e2LwA==" crossorigin="anonymous" referrerpolicy="no-referrer" />
</svelte:head>

<script>
	let classes = "button is-link";
	let text = "Do"
	let lastState = NaN;
	
	function doStuff() {
		text = "Doing";
		lastState = NaN;
		new Promise((res, rej) => {
			setTimeout(() => {
				if(Math.random() > 0.5) {
					res();
				} else {
					rej(new Error("Not successful"));
				}
			}, 200)
		})
		.then(() => {
			lastState = 1;
		})
		.catch((e) => {
			lastState = 0;
		});
		// .finally(() => {
		// 	lastState = NaN;
		// 	text = "Do";
		// })
	}
</script>
<button class={classes} on:click={doStuff}>
	{#if !isNaN(lastState)}
		{#if  lastState === 0}
			 <i class="fa-solid fa-check"></i>
		{:else if lastState === 1}
			<i class="fa-solid fa-x"></i>
		{/if}
		&nbsp;
	{/if}
	{text}
</button>
