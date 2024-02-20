<svelte:head>
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@0.9.4/css/bulma.min.css">
	<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css" integrity="sha512-DTOQO9RWCH3ppGqcWaEA1BIZOC6xxalwEsw9c2QQeAIftl+Vegovlnee1c9QX4TctnWMn13TZye+giMm8e2LwA==" crossorigin="anonymous" referrerpolicy="no-referrer" />
</svelte:head>
<script>
	import Nested from './Nested.svelte';
</script>


<Nested promiseFunc={() => new Promise((res, rej) => {
			setTimeout(() => {
				if(Math.random() > 0.5) {
					res();
				} else {
					rej(new Error("Not successful"));
				}
			}, 200)
		})}
	on:success={() => {console.log("success")}}
	on:failure={() => {console.log("failure")}}/>




