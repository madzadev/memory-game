<script>
import Card from './Card.svelte';

let first = '';
let second = '';

const compare =(a, b)=>{
	if(a===b){
console.log('images match')
	}
}

const cardClickHandler = (e) => {
	if(first==''){
first = e.target.currentSrc;
	} else {
second = e.target.currentSrc;
compare();
	}
	
}



</script>

<main>
	<h1>Svelte Memory Card game</h1>
	<Card title={"?"} image={"https://source.unsplash.com/random/300x200"} onClick={cardClickHandler}/>
</main>

<style>
	h1 {
		text-align: center;
	}

	main {
		max-width: 800px;
		margin: 0 auto;
	}
</style>