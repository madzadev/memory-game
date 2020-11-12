<script>
  export let title, image, onClick, active;
</script>

<style>
  .flip-card {
    background-color: transparent;
    width: 200px;
    height: 150px;
    perspective: 1000px; /* Remove this if you don't want the 3D effect */
    cursor: pointer;
  }

  /* This container is needed to position the front and back side */
  .flip-card-inner {
    position: relative;
    width: 100%;
    height: 100%;
    text-align: center;
    transition: transform 0.5s;
    transform-style: preserve-3d;
  }

  .active {
    transform: rotateY(180deg);
  }
  /* .flip-card:hover .flip-card-inner {
    transform: rotateY(180deg);
  } */
  /* h1 {
    z-index: -11;
  } */
  /* Position the front and back side */
  .flip-card-front,
  .flip-card-back {
    position: absolute;
    width: 100%;
    height: 100%;
    -webkit-backface-visibility: hidden; /* Safari */
    backface-visibility: hidden;
  }

  /* Style the front side (fallback if image is missing) */
  .flip-card-front {
    background-color: dodgerblue;
    color: white;
    display: grid;
    place-items: center; /*to center the back of cards */
  }

  /* Style the back side */
  .flip-card-back {
    transform: rotateY(180deg);
    background-color: #bbb;
    color: black;
  }
</style>

<div class="flip-card" on:click={onClick}>
  <div class={!active ? 'flip-card-inner' : 'flip-card-inner active'}>
    <div class="flip-card-front">
      <h1>{title}</h1>
    </div>
    <div class="flip-card-back"><img src={image} alt="alt" /></div>
  </div>
</div>
