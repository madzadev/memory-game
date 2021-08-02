<script>
  import Card from "./Card.svelte";

  // Controls
  const cards = 12;
  const theme = "animals";

  //   Generate numbers Schwartzian transform method
  let arr = [...Array(cards / 2).keys()]
    .map((i) => i + 1)
    .flatMap((i) => [i, i])
    .map((a) => ({
      sort: Math.random(),
      value: a,
    }))
    .sort((a, b) => a.sort - b.sort)
    .map((a) => a.value);

  let firstChoice = "";
  let secondChoice = "";

  let openCards = [];

  let message = "Open cards!";

  let guesses = 0;
  let matches = 0;

  const compare = (a, b) => {
    ++guesses;
    if (
      a.nextElementSibling.firstChild.currentSrc ===
      b.nextElementSibling.firstChild.currentSrc
    ) {
      ++matches;
      openCards.push(parseInt(a.innerText), parseInt(b.innerText));
      if (cards / 2 == matches) {
        message = "You won!";
      } else {
        message = "Found a match!";
      }

      firstChoice = "";
      secondChoice = "";
    } else {
      message = "No match!";
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
    if(!firstChoice) {
      firstChoice = e.target;
    } else {
      secondChoice = e.currentTarget.firstChild.firstChild;
      if(firstChoice!==secondChoice) {
        compare(firstChoice, secondChoice);
      } else {
        firstChoice='';
        secondChoice='';
      }
    }
  };
</script>

<style>
  h1 {
    text-align: center;
  }

  main {
    max-width: 1200px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(270px, 1fr));;
    gap: 30px;
    place-items: center;
  }

</style>

<h1>Memory Cards</h1>
<main>
{#each arr as card, i}
    <Card
      title={i + 1}
      image={`https://source.unsplash.com/random/260x200?${card}?${theme ? theme : ''}`}
      onClick={cardClickHandler}
      active={openCards.includes(i + 1) || firstChoice.innerText == i + 1 || secondChoice.innerText == i + 1} />
  {/each}
  <p>Guesses: {guesses}</p>
  <p>Matches: {matches}</p>
  <p>Percentage: {guesses != 0 ? Math.round((matches * 100) / guesses) : 0}%</p>
  <p>{message}</p>
</main>
