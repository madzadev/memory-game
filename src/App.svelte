<script>
import Card from "./Card.svelte";

//   Generate numbers Schwartzian transform method
const cards = 8;

let arr = [...Array(cards).keys()]
   .map((i) => i + 1)
   .flatMap((i) => [i, i])
   .map((a) => ({
      sort: Math.random(),
      value: a
   }))
   .sort((a, b) => a.sort - b.sort)
   .map((a) => a.value);

let firstChoice = "";
let secondChoice = "";

let openCards = [];

let guesses = 0;
let matches = 0;

const compare = (a, b) => {
   ++guesses;
   if (
      a.nextElementSibling.firstChild.currentSrc ===
      b.nextElementSibling.firstChild.currentSrc
   ) {
      console.log("Found a match");
      openCards.push(parseInt(a.innerText), parseInt(b.innerText));
      ++matches;
      firstChoice = "";
      secondChoice = "";
   } else {
      reset();
   }
};

const reset = () => {
   setTimeout(() => {
      firstChoice = "";
      secondChoice = "";
   }, 800);
};

const cardClickHandler = (e) => {
   if (secondChoice == '') {
      if (firstChoice == "") {
         firstChoice = e.target;
         console.log("first click");
         console.log(e);
         console.log(firstChoice)
      } else {
         secondChoice = e.target;
         console.log("second click");
         console.log(secondChoice)
         compare(firstChoice, secondChoice);
      }
   } else {
		secondChoice = "";
		firstChoice = "";
		firstChoice = e.target;
	}

};
</script>

<style>
h1 {
   text-align: center;
}

main {
   max-width: 1000px;
   margin: 0 auto;
   display: grid;
   grid-template-columns: repeat(4, 1fr);
   gap: 20px;
}
</style>

<h1>Svelte Memory Cards</h1>
<main>
  {#each arr as card, i}
    <Card
      title={i + 1}
      image={`https://source.unsplash.com/random/200x150?${card}`}
      onClick={cardClickHandler}
      active={openCards.includes(i + 1) || firstChoice.innerText == i + 1 || secondChoice.innerText == i + 1} />
  {/each}
  <p>Guesses: {guesses}</p>
  <p>Matches: {matches}</p>
  <p>Percentage: {guesses!=0?Math.round((matches * 100) / guesses):0}%</p>
  <p>{cards==matches?'Congrats you won!':''}</p>
</main>
