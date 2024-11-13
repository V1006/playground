<template>
    <div
        id="main"
        class="w-full h-screen bg-gray-100 flex flex-row bg-cover bg-center bg-no-repeat relative overflow-hidden"
        @mousemove="handleMousemove"
    >
        <div class="key-visuals">
            <div class="background-image-a">
                <picture>
                    <img class="background-light" src="public/girl.jpeg" />
                </picture>
            </div>
            <div
                class="background-image-b"
                @click="handleClick(mouseX, mouseY)"
            >
                <picture>
                    <img
                        class="background-dark"
                        src="public/girl-inverted.png"
                        :style="`mask-position: ${mouseX} ${mouseY}`"
                    />
                </picture>
                <div
                    class="key-enter absolute"
                    :style="`transform: translate(calc(${mouseX} + 18vh ),calc(${mouseY} + 20vh))`"
                >
                    ENTER
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { ref, onMounted, onUnmounted } from "vue";

const circleSize = 400;
let mouseX = ref("0px");
let mouseY = ref("0px");

const handleMousemove = (e) => {
    setTimeout(() => {
        mouseX.value = e.clientX - circleSize / 2 + "px";
        mouseY.value = e.clientY - circleSize / 2 + "px";
    }, 50);
};

export default {
    setup() {
        const handleClick = (x, y) => {
            console.log(parseInt(x, 10));
            console.log(mouseX, mouseY);
            const element = document.querySelector("#main");
            const mask = document.querySelector(".background-dark");

            element.removeEventListener("mousemove", handleMousemove);
            /*     mask.style = `mask-position: ${parseInt(x, 10) - 200} ${
                parseInt(y, 10) - 200
            };`; */
            mask.style = `mask-position: center`;
            document.querySelector(".key-enter").classList.add("key-click");

            mask.classList.add("mask-click");
        };

        onMounted(() => {
            const element = document.querySelector("#main");
            element.addEventListener("mousemove", handleMousemove);
        });

        onUnmounted(() => {
            const element = document.querySelector("#main");
            element.removeEventListener("mousemove", handleMousemove);
        });

        return { mouseX, mouseY, handleClick };
    },
};
</script>

<style>
#main {
    cursor: pointer;
    font-family: Arial, Helvetica, sans-serif;
    font-weight: 700;
    color: white;
}

.background-image-a {
    z-index: 1;
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100vh;
}

.background-light {
    z-index: 1;
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100vh;
    object-fit: cover;
    object-position: center;
}

.background-image-b {
    z-index: 2;
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100vh;
}

.background-dark {
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100vh;
    object-fit: cover;
    object-position: center;
    mask-image: url("public/circle-blur.webp");
    mask-repeat: no-repeat;
    mask-size: 50vh 50vh;
}

.key-enter {
    top: 0;
    left: 0;
    font-size: 4vh;
    opacity: 1;
}

.key-click {
    opacity: 0;
    transition: opacity 1s ease;
}

.mask-click {
    /* mask-position: center; */
    mask-size: 300vh 300vh;
    transition: mask-size 1s ease-in, mask-position 1s ease-in;
}
</style>
