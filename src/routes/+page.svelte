<script lang="ts">
	import Row from "$lib/row.svelte";
    import { json } from "@sveltejs/kit";
	import { browser } from "$app/environment";
	import Button from "$lib/button.svelte";
	interface leaderboardRow {
		yearGroup:string,
		score:number,
		correctGuesses:number
	}
	//TODO doesnt update initially
	let leaderboardTemp : leaderboardRow = {
		'yearGroup' : 'Year 12',
		'score' : 0,
		'correctGuesses' : 0
	}
	let leaderboard:Array<leaderboardRow> | null | string =[]
	if (browser){
		leaderboard = JSON.parse(localStorage.getItem('leaderboard'))
		if(!leaderboard){
			let leaderboardNew = [
				{'yearGroup':'Year 12','score':0,'correctGuesses':0},
				{'yearGroup':'Year 13','score':0,'correctGuesses':0},
				{'yearGroup':'Year 11','score':0,'correctGuesses':0},
				{'yearGroup':'Year 10','score':0,'correctGuesses':0},
				{'yearGroup':'Year 9','score':0,'correctGuesses':0},
				{'yearGroup':'Year 7','score':0,'correctGuesses':0},
				{'yearGroup':'Year 8','score':0,'correctGuesses':0}
			]
			localStorage.setItem('leaderboard',JSON.stringify(leaderboardNew))
		}
		console.log(leaderboard)
	}

	const addScore = (score:number,index:number) => {
		leaderboard[index].score += score
		leaderboard[index].correctGuesses += 1
		leaderboard.sort((a, b) => b.score - a.score);
		console.log(leaderboard[index].score)
		localStorage.setItem('leaderboard',JSON.stringify(leaderboard))
	}
</script>
<main class="w-full h-screen flex items-center justify-center">
	<div class="w-[80vw] h-fit rounded-lg shadow-md border-2 border-gray-300 divide-y">
		<Row firstColumn='Year group' secondColumn='Score' thirdColumn='Correct guesses' backgroundColor='slate' firstRow/>
		{#each leaderboard as i,index}
			<Row firstColumn={i?.yearGroup} secondColumn={i.score} thirdColumn={i.correctGuesses} fn={()=>{addScore(5,index)}}/>
		{/each}
	</div>
</main>