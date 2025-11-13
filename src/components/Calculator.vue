<script setup lang="ts">
import { ref } from "vue"
import isIpValid from "./isIpValid"
import getNetworkAdress from "./getNetworkAdress"
import getAddressesCount from "./getAddressesCount"
import options from "./options"

const ip = ref('')
const mask = ref('255.255.255.255')
const isShowResult = ref(false)

function showResult() {
    isShowResult.value = true
}
</script>

<template>
    <h1>Калькулятор подсетей</h1>
    <form @submit.prevent="showResult()" class="form">
        <input v-model="ip" class="input" />

        <select v-model="mask" class="select">
            <option v-for="option in options" :key="option" :value="option">{{ option }}</option>
        </select>

        <button type="submit" :disabled="!isIpValid(ip)">Рассчитать</button>
    </form>
    <div v-if="isShowResult && isIpValid(ip)" class="result">
        <h2 class="h2">Результат</h2>
        <div>IP: {{ ip }}</div>
        <div>Маска подсети: {{ mask }}</div>
        <div>IP-адрес сети: {{ getNetworkAdress(ip, mask) }}</div>
        <div>Количество адресов: {{ getAddressesCount(mask) }}</div>
    </div>
</template>