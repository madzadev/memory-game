<script>
  import Card from "./Card.svelte";

  let firstChoice = "";
  let secondChoice = "";

  let openCards = [];

  const compare = (a, b) => {
    if (a.currentSrc === b.currentSrc) {
      openCards.push(parseInt(a.innerText), parseInt(b.innerText));
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
    } else {
      secondChoice = e.target;
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
  {#each { length: 16 } as card, i}
    <Card
      title={i + 1}
      image={'https://source.unsplash.com/random/200x150'}
      onClick={cardClickHandler}
      active={openCards.includes(i + 1) || (firstChoice && firstChoice.innerText == i + 1) || (secondChoice && secondChoice.innerText == i + 1)} />
  {/each}
</main>
