<script>
  import Card from "./Card.svelte";

  //   Generate numbers Schwartzian transform method
  let arr = [...Array(8).keys()]
    .map((i) => i + 1)
    .flatMap((i) => [i, i])
    .map((a) => ({ sort: Math.random(), value: a }))
    .sort((a, b) => a.sort - b.sort)
    .map((a) => a.value);

  let firstChoice = "";
  let secondChoice = "";

  let openCards = [];

  let guesses = 0;
  let matches = 0;

  const compare = (a, b) => {
    ++guesses;
    console.log(a.currentSrc, b.currentSrc);
    if (a.currentSrc === b.currentSrc) {
      console.log("Found a match");
      openCards.push(parseInt(a.innerText), parseInt(b.innerText));
      ++matches;
    }
  };

  const reset = (a, b) => {
    setTimeout(() => {
      a = "";
      b = "";
    }, 1000);
  };

  const cardClickHandler = (e) => {
    if (firstChoice == "") {
      firstChoice = e.target;
      console.log(e);
    } else {
      secondChoice = e.target;
      console.log("second click");
      compare(firstChoice, secondChoice);
      reset(firstChoice, secondChoice);
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

<h1>Svelte Memory Card game</h1>
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
  <p>Percentage: {(matches * 100) / guesses}</p>
</main>
