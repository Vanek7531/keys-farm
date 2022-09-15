<script setup>
import { ref, watch } from "vue";

import html2canvas from "html2canvas";

const letter = ref("");

const some = ref("");

const imageToFile = ref(null);

let img = ref(null);

const screenShot = () => {
    console.log("screenShot");
    let a = Number(imageToFile.value.style.width.slice(0, 3));
    let b = Number(imageToFile.value.style.height.slice(0, 3));

    html2canvas(imageToFile.value, {
        // width:
        //     a ||
        //     window.innerWidth ||
        //     document.documentElement.clientWidth ||
        //     document.body.clientWidth,
        // height:
        //     b ||
        //     window.innerHeight ||
        //     document.documentElement.clientHeight ||
        //     document.body.clientHeight,
        width: 900,
        height: 400,
    }).then((canvas) => {
        // Первый параметр - это элемент, который должен создать снимок экрана, а второй - параметр, который вам нужно настроить, ширина, высота и т. д.
        img.value = canvas.toDataURL("image/png");
    });
};

const temp = () => {
    console.log("покинули ЧАТ?");
};

const blurOf = ref(false);

watch(letter, (newVal) => {
    // if ((letter.value = newVal)) console.log("=", letter.value);

    // if (letter.value == newVal && blurOf.value == true) {
    //     console.log("проходит 2");
    //      screenShot();
    // }
    setTimeout(function () {
        if (letter.value == newVal && blurOf.value !== false) {
            screenShot();
        }
    }, 3000);
    // setTimeout(function () {
    //     letter.value = newVal;
    //     some.value = letter.value;
    // }, 2000);
});

// watch([letter, watchForRoutePath], ([newVal, newVal2]) => {
//     if (letter.value === newVal && blurOf.value === newVal2) console.log("123");
// });
</script>

<template>
    <div class="container">
        <p>{{ blurOf }}</p>
        <div>
            <textarea
                style="width: 80%; height: 100%; padding: 20px"
                id="imageToFile"
                name="someName"
                cols="30"
                rows="10"
                v-model="letter"
                @blur="(blurOf = false), screenShot()"
                @focus="blurOf = true"
            ></textarea>

            <br />
            <p
                ref="imageToFile"
                style="
                    width: 800px;
                    height: 300px;
                    padding: 50px;
                    margin: 0 auto;
                    text-align: start;
                "
            >
                {{ letter }}
            </p>
            <img id="new_img" :src="img" v-if="img" />
        </div>
    </div>
</template>

<style lang="scss" scoped>
.container {
    overflow-y: scroll;
    // height: calc(100% - 78px);
    height: 700px;
    padding-bottom: 200px;
}
textarea {
    border-radius: 20px;
    background: grey;
    color: #42b983;
    font-size: 26px;
}
p {
    font-size: 26px;
    margin-top: 15px;
    color: rgb(218, 212, 212);
}
</style>
