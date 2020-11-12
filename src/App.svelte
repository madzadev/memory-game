<script>
  import Card from "./Card.svelte";

  let first = "";
  let second = "";

  let number = 0;

  const compare = (a, b) => {
    if (a === b) {
      console.log("images match");
    }
  };

  const reset = () => {
    first = "";
    second = "";
  };

  const cardClickHandler = (e) => {
    number = e.target.innerText;
    if (first == "") {
      first = e.target.currentSrc;
    } else {
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
      active={number == index + 1 ? true : false} />
  {/each}
</main>
