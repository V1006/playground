<template>
    <div class="effect-container">
        <div class="flex">
            <img
                src="https://images.pexels.com/photos/7668066/pexels-photo-7668066.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1"
                alt="the back of random person"
            />
            <img
                src="https://images.pexels.com/photos/28714404/pexels-photo-28714404/free-photo-of-honey-drizzle-from-wooden-dipper-on-yellow-background.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1"
                alt="an eagle"
                style="--f: 0.12; --r: 5px"
            />
            <img
                src="https://assets.codepen.io/1480814/pexels-pixabay-62655.jpg"
                alt="a cup of something to drink, probably some tea"
                style="--f: 0.08; --r: 20px"
            />
        </div>
    </div>
</template>
<!-- the type of image is important for the illusion 
   use an image having the main element in the center and a uniform background
-->

<script>
import { ref, onMounted, onUnmounted } from "vue";
</script>

<style>
img {
    --f: 0.1; /* the parallax factor (the smaller the better) */
    --r: 10px; /* radius */

    --_f: calc(100% * var(--f) / (1 + var(--f)));
    --_a: calc(90deg * var(--f));
    width: 300px; /* the image size */
    aspect-ratio: calc(1 + var(--f));
    object-fit: cover;
    clip-path: inset(0 var(--_f) 0 0 round var(--r));
    transform: perspective(400px) var(--_t, rotateY(var(--_a)));
    transition: 0.5s;
    cursor: pointer;
}
img:hover {
    clip-path: inset(0 0 0 var(--_f) round var(--r));
    --_t: translateX(calc(-1 * var(--_f))) rotateY(calc(-1 * var(--_a)));
}

.effect-container {
    margin: 0;
    min-height: 100vh;
    display: grid;
    place-content: center;
    grid-auto-flow: column;
    gap: 30px;
    background: #a8313d;
}
</style>
