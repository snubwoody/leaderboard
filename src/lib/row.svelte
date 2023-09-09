<script lang='ts'>
	import Button from "./button.svelte";

	export let backgroundColor:colors = 'white'
	export let firstColumn:any;
	export let secondColumn:any;
	export let thirdColumn:any;
	export let fn:any;
	export let firstRow:boolean =  false;
	
	type colors = 'gray' | 'white'

	const backgroundColors = {
		'gray' : 'bg-gray-300',
		'white' : 'bg-white',
		'slate' : 'bg-[#2A363B] text-white'
	}

	let borderRadius = firstRow ? 'rounded-t-2' : ''
</script>

<div class={`w-full h-14 ${backgroundColors[backgroundColor]} flex ${borderRadius} divide-x-2 relative items-center`}>
	<div class="w-1/3 h-full flex items-center justify-center">{firstColumn}</div>
	<div class="w-1/3 h-full flex items-center justify-center">{secondColumn}</div>
	<div class="w-1/3 h-full flex items-center justify-center">{thirdColumn}</div>
	{#if !firstRow}
		<Button fn={fn} text=''/>
	{/if}
</div>