<script lang="ts">
import { ref } from "vue";
import { Options, Vue } from "vue-class-component";

@Options({
    props: {
        msg: String,
    },
})
export default class HelloWorld extends Vue {
    msg!: string;
}
</script>

<template>
    <div class="hello">
        <h1>{{ msg }}</h1>
        <textarea name="someName" id="someName" cols="30" rows="10"></textarea>
    </div>
</template>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
textarea {
    width: 60%;
    height: 400px;
    border-radius: 20px;
    background: grey;
    color: #42b983;
    font-size: 26px;
    padding: 20px;
}

h3 {
    margin: 40px 0 0;
}
ul {
    list-style-type: none;
    padding: 0;
}
li {
    display: inline-block;
    margin: 0 10px;
}
a {
    color: #42b983;
}
</style>
