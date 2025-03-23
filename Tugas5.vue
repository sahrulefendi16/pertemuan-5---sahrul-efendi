<script setup>
import { ref, computed, watch, onMounted } from 'vue';

const daftarBuah = ref(['Apel', 'Mangga', 'Jeruk', 'Pisang', 'Nanas'])

const firstName = ref('')
const laseName = ref('')

const fullName = computed(() => {
    return firstName.value && lastName.value
    ? `${firstName.value} ${laseName.value}`
    : `Silahkan isi nama`
})

const searchQuery = ref('')
const searchStatus = ref('Menunggu input...')

watch(searchQuery, (newValue, oldValue) => {
    if (newValue.trim() === '') {
        searchStatus.value = 'Menunggu input...'
    } else {
        searchStatus.value = `Mencari: ${newValue}`
    }
})

const inputElement = ref(null)

function focusInput() {
    inputElement.value
}

onMounted(() => {
    inputElement.value.focus()
    console.log('Komponen telah dimuat')
})
</script>

<template>
<ul>
    <li v-for="(buah, index) in daftarBuah" :key="index">
        {{ index + 1 }}. {{ buah }}
    </li>
</ul>

<div>
    <input v-model="firstName" placeholder="Nama depan" />
    <input v-model="lastName" placeholder="Nama belakang" />
    <p>nama lengkap: {{ fullName }}</p>
</div>

<div>
    <input v-model="searchQuery" placeholder="Cari..."/>
    <p>{{ searchStatus }}</p>
</div>

<div>
    <input ref="inputElement" placeholder="Focus otomatis" />
    <button @click="focusInput">Focus kembali</button>
</div>
</template>

<style scoped>

</style>