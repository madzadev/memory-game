<script>
  import Card from "./Card.svelte";

  const cards = 12;
  const theme = "nature";

  let firstChoice = "",
    secondChoice = "",
    openCards = [],
    activeOpen = "",
    message = "Open cards!",
    guesses = 0,
    matches = 0,
    loading = false;

  const prepareArray = (cards) =>
    [...Array(cards / 2).keys()]
      .map((i) => i + 1)
      .flatMap((i) => [i, i])
      .map((a) => ({
        sort: Math.random(),
        value: a,
      }))
      .sort((a, b) => a.sort - b.sort)
      .map((a) => a.value);

  let arr = prepareArray(cards);

  const compare = (a, b) => {
    loading = true;
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
      loading = false;
    } else {
      message = "No match!";
      reset();
    }
  };

  const reset = () => {
    setTimeout(() => {
      firstChoice = "";
      secondChoice = "";
      loading = false;
      activeOpen = "";
    }, 800);
  };

  const resetGame = async () => {
    arr = prepareArray(cards);

    (firstChoice = ""),
      (secondChoice = ""),
      (openCards = []),
      (message = "Open cards!"),
      (guesses = 0),
      (matches = 0);
  };

  const cardClickHandler = (e) => {
    const isOpened = openCards.includes(
      Number(e.currentTarget.firstChild.firstChild.innerText)
    );
    const isActiveOpen =
      Number(activeOpen) ==
      Number(e.currentTarget.firstChild.firstChild.innerText);

    e.preventDefault();
    if (!loading && !isOpened && !isActiveOpen) {
      if (!firstChoice) {
        firstChoice = e.currentTarget.firstChild.firstChild;
      } else {
        secondChoice = e.currentTarget.firstChild.firstChild;
        compare(firstChoice, secondChoice);
      }
    }

    activeOpen = e.currentTarget.firstChild.firstChild.innerText;
  };
</script>

<h1>Memory Cards</h1>
<main id="main">
  {#each arr as card, i}
    <Card
      title={i + 1}
      image={` https://unsplash.it/560/320?random?${card}?${
        theme ? theme : ""
      }`}
      
      onClick={cardClickHandler}
      active={openCards.includes(i + 1) ||
        firstChoice.innerText == i + 1 ||
        secondChoice.innerText == i + 1}
    />
  {/each}
  <p>Guesses: {guesses}</p>
  <p>Matches: {matches}</p>
  <p>
    Percentage: {guesses != 0 ? Math.round((matches * 100) / guesses) : 0}%
  </p>
  <p>{message}</p>
</main>
{#if message == "You won!"}
  <p id="reset" on:click={resetGame}>Reset</p>
{/if}

<style>
  :global(body) {
    padding: 20px;
  }
  h1 {
    text-align: center;
    margin-bottom: 50px;
  }

  main {
    max-width: 1200px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 30px;
    place-items: center;
  }

  p {
    font-size: 18px;
  }

  #reset {
    text-align: center;
    cursor: pointer;
  }
</style>
