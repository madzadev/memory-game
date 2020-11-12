<script>
  import Card from "./Card.svelte";

  let first = "";
  let second = "";

  let firstNum = 0;
  let secondNum = 0;

  let openCards = [];

  const compare = (a, b) => {
    if (a === b) {
      console.log("images match");
      openCards.push(firstNum, secondNum);
      console.log(`open array is: ${openCards}`);
    }
  };

  const reset = () => {
    setTimeout(() => {
      first = "";
      second = "";
      firstNum = 0;
      secondNum = 0;
    }, 1000);
  };

  const cardClickHandler = (e) => {
    if (first == "") {
      firstNum = e.target.innerText;
      first = e.target.currentSrc;
    } else {
      secondNum = e.target.innerText;
      second = e.target.currentSrc;
      compare();
      reset();
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
  {#each { length: 16 } as card, index}
    <Card
      title={index + 1}
      image={'https://source.unsplash.com/random/200x150'}
      onClick={cardClickHandler}
      active={openCards.includes(index + 1) || firstNum == index + 1 || secondNum == index + 1} />
  {/each}
</main>
