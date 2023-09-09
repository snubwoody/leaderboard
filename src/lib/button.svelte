<script lang='ts'>
	import add from '$lib/assets/add.svg'
	export let text:string;
	export let fn:any;
</script>

<button
	 class="w-9 h-9 rounded-md bg-white border-2 border-gray-300 shadow-md flex items-center justify-center absolute right-[-50px]" 
	on:click={fn}
	>
		<img src={add} alt="Add button">
</button>