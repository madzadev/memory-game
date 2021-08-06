<script>
export let title, image, onClick, active;
</script>

<style>
.flip-card {
   background-color: transparent;
   width: 260px;
   height: 200px;
   perspective: 1000px;
   cursor: pointer;
}

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

.flip-card-front,
.flip-card-back {
   position: absolute;
   width: 100%;
   height: 100%;
   -webkit-backface-visibility: hidden;
   backface-visibility: hidden;
}

.flip-card-front {
   background-color: dodgerblue;
   background: url('https://source.unsplash.com/random/260x200?white');
   color: white;
   display: grid;
   place-items: center;
}

.flip-card-back {
   transform: rotateY(180deg);
   background-color: #bbb;
   color: black;
}
</style>

<div class="flip-card" on:click={onClick} >
    <div class={!active ? 'flip-card-inner' : 'flip-card-inner active'}>
        <div class="flip-card-front">
            <h1>{title}</h1>
        </div>
        <div class="flip-card-back"><img class="image" src={image} alt="alt" /></div>
    </div>
</div>
