<script setup>
import { computed, onMounted, ref, watch } from "vue";

import html2canvas from "html2canvas";

const letter = ref("");

const some = ref(null);

const imageToFile = ref(null);

let img = ref(null);

const onLoad = ref(false);

const result = ref("");

const someTextConst = ref("");

// const imageToFileComp = computed(() => {
//     if (onLoad.value) {
//         console.log("computed");
//         return some.value.outerText;
//     } else return "nothing";
// });

const screenShot = () => {
    // console.log("result", result.value);
    console.log("screenShotTEXT:", some.value.outerText);
    // console.log("screenShot");

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
        width: 325,
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
    // setTimeout(function () {
    //     if (letter.value == newVal && blurOf.value !== false) {
    //         screenShot();
    //     }
    // }, 3000);
    // setTimeout(function () {
    //     letter.value = newVal;
    //     some.value = letter.value;
    // }, 2000);
});

// watch([letter, watchForRoutePath], ([newVal, newVal2]) => {
//     if (letter.value === newVal && blurOf.value === newVal2) console.log("123");
// });

// document.getElementById("imageToFile").addEventListener(
//     "input",
//     function () {
//         console.log("123123");
//     },
//     false
// );

const res = ref(null);

const somePromiseFunc = async () => {
    res.value = await some.value;
    let searchtimer;
    if (res.value) {
        return res.value.addEventListener(
            "input",
            () => {
                clearTimeout(searchtimer);
                searchtimer = setTimeout(() => {
                    screenShot();
                }, 3000);
            },
            false
        );
    }
};

// if (some.value !== null) {
//     console.log("123123");
//     some.value.addEventListener("input",  ()=> {}, false);
// }

// let firstPromise = new Promise((resolve, reject) => {
//     resolve((some.value = document.getElementById("imageToFile")));
// });

// firstPromise.then((result) => {
//     console.log("res123", result);
// });

onMounted(() => {
    some.value = document.getElementById("imageToFile");
    if (imageToFile.value) onLoad.value = true;
});
</script>

<template>
    <div class="container">
        <p v-if="somePromiseFunc()">{{ somePromiseFunc() }}</p>

        <div>
            <input
                type="text"
                contenteditable="true"
                style="width: 80%; height: 100%; padding: 20px; margin: 0 auto"
                id="imageToFile"
                name="someName"
                cols="30"
                rows="10"
                @blur="(blurOf = false), screenShot()"
                @focus="blurOf = true"
                class="text-area"
                ref="imageToFile"
                v-model="letter"
                v-if="false"
            />
            <!-- contenteditable="true" -->
            <div
                contenteditable="true"
                style="
                    width: 80%;
                    height: 100%;
                    padding: 20px;
                    margin: 0 auto;
                    position: relative;
                "
                id="imageToFile"
                name="someName"
                @blur="(blurOf = false), screenShot()"
                @focus="blurOf = true"
                class="text-area"
                ref="imageToFile"
            >
                <textarea
                    style="width: 96%; height: 100%; padding: 20px"
                    id="imageToFile"
                    name="someName"
                    cols="30"
                    rows="10"
                    v-model="letter"
                    @blur="(blurOf = false), screenShot()"
                    @focus="blurOf = true"
                    v-if="false"
                ></textarea>
                <!-- {{ letter }} -->
            </div>
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
                v-if="false"
            >
                {{ letter }} // {{ imageToFile.value.outerText }} //
                {{ imageToFileComp }} // {{ some }} // {{ result }}
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
    font-size: 16px !important;
}
textarea {
    font-size: 16px !important;
    border-radius: 10px;
    background: transparent;
    color: transparent;
    font-size: 26px;
    position: absolute;
    // color: wheat;
    left: 0;
    // font-size: 1px;s
    top: 0;
    border: 1px solid black;
    &:focus {
        border: none;
        outline: none;
    }
}
p {
    font-size: 26px;
    margin-top: 15px;
    color: rgb(218, 212, 212);
}

.text-area {
    font-size: 16px !important;
    background: wheat;
    margin: 0 auto;
    min-height: 300px;
    border-radius: 10px;
    text-align: left;
}
</style>
