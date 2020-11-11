<script>
   export let title, image, onClick;
</script>

<div class="flip-card" on:click={onClick}>
  <div class="flip-card-inner">
    <div class="flip-card-front">
       <h1>{title}</h1>
    </div>
    <div class="flip-card-back">
      <img src={image} alt="Avatar">
    </div>
  </div>
</div>

<style>
.flip-card {
  background-color: transparent;
  width: 300px;
  height: 200px;
  border: 1px solid #f1f1f1;
  perspective: 1000px; /* Remove this if you don't want the 3D effect */
  cursor: pointer;
}

/* This container is needed to position the front and back side */
.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}

/* Do an horizontal flip when you move the mouse over the flip box container */
.flip-card:hover .flip-card-inner {
  transform: rotateY(180deg);
}

/* Position the front and back side */
.flip-card-front, .flip-card-back {
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
}

/* Style the back side */
.flip-card-back {
  transform: rotateY(180deg);
  background-color: #bbb;
  color: black;
}
</style>