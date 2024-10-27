<template>
    <div class="container">
        <button @click="getFact">Click for a fact</button>
        <div class="textBox">        
            <p>{{ fact }}</p>
        </div>
    </div>
</template>

<script lang="ts">
import { get } from 'http';
import {ref} from 'vue';

const fact = ref<string>("This is a fact");

async function getFact() {
    const response = await fetch("https://uselessfacts.jsph.pl/random.json?language=en");
    const data = await response.json() as { text: string };
    fact.value = data.text;
    }
    export default {
        data() {
            return {
                fact
            }
        },
        methods: {
            getFact
        }
};
</script>

<style scoped>
.container{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 100vh;
}
.textBox{
    display: flex;
    position: fixed;
    top: 10px;
    flex-direction: column;
    text-align: center;
    padding: 10px;
    background-color: gray;
    border-radius: 10px;
    color: black;
}
button {
    background-color: #ffffff;
    border: 3px solid #6c1818;
    border-radius: 10px;
    padding: 15px 32px;
    text-align: center;
    font-size: 16px;
}
</style>