<script>
  import Card from "./Card.svelte";

  let first = "";
  let second = "";

  let firstNum = 0;
  let secondNum = 0;

  let open = [];

  const compare = (a, b) => {
    if (a === b) {
      console.log("images match");
      open.push(firstNum, secondNum);
      console.log(`open array is: ${open}`);
    }
  };

  const reset = () => {
    first = "";
    second = "";
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
      active={open.includes(index + 1) || firstNum == index + 1 || secondNum == index + 1} />
  {/each}
</main>
