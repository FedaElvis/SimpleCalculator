<script setup>
import {computed, ref} from 'vue'

const display = ref('0')

const appendToDisplay = (value) =>{
if(display.value == 0 && value != '.')
display.value = value
else{
    display.value += value
}
}

//function to calculate
const calculate = () =>{
    try {
        display.value = eval(display.value)
    } catch (error) {
        display.value = 'error'
    }
}

//function to clear display
const clearDisplay = () =>{
    display.value = ''
}

//computed property for dynamic class binding

const displayClass = computed(() =>{
return display.value.length > 12 ? 'small-text' : ''
})

</script>

<template>
    <div class="calculator">
        <input type="text" v-model="display" :class="displayClass" readonly>
        <div class="buttons">
            <button @click="appendToDisplay('7')">7</button>
            <button @click="appendToDisplay('9')">8</button>
            <button @click="appendToDisplay('9')">9</button>
            <button @click="appendToDisplay('/')">/</button>

            <button @click="appendToDisplay('4')">4</button>
            <button @click="appendToDisplay('5')">5</button>
            <button @click="appendToDisplay('6')">6</button>
            <button @click="appendToDisplay('*')">*</button>

            <button @click="appendToDisplay('1')">1</button>
            <button @click="appendToDisplay('2')">2</button>
            <button @click="appendToDisplay('3')">3</button>
            <button @click="appendToDisplay('-')">-</button>

            <button @click="appendToDisplay('0')">0</button>
            <button @click="appendToDisplay('.')">.</button>
            <button @click="calculate">=</button>
            <button @click="appendToDisplay('+')">+</button>
        </div>
        <button @click="clearDisplay" class="clear-button">C</button>
    </div>
</template>

<style scoped>
.calculator {
    width: 320px;
    margin: 0 auto;
    background: #f7f7f7;
    border-radius: 20px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    padding: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
}

input[type="text"] {
    width: 100%;
    height: 80px;
    background: #fff;
    border: 1px solid #ddd;
    border-radius: 15px;
    text-align: right;
    font-size: 2em;
    padding: 10px;
    box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.1);
    margin-bottom: 10px;
}

.buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
}

button {
    background: #f0f0f0;
    border: none;
    border-radius: 15px;
    font-size: 1.5em;
    padding: 20px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    cursor: pointer;
    transition: background 0.2s, box-shadow 0.2s;
}

button:active {
    background: #e0e0e0;
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
}

button.operator {
    background: #ff9500;
    color: #fff;
}

button.operator:active {
    background: #e89e00;
}

.clear-button {
    width: 100%;
    background: #ff3b30;
    color: #fff;
    border: none;
    border-radius: 15px;
    font-size: 1.5em;
    padding: 20px;
    cursor: pointer;
    transition: background 0.2s;
}

.clear-button:active {
    background: #e0301e;
}

.small-text {
    font-size: 0.5em;
}
</style>


