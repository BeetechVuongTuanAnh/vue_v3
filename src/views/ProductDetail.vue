<script setup lang="ts">
import { ref } from 'vue';
import { useRoute } from 'vue-router'

const route = useRoute();

interface ProductsType {
    'id': number,
    'name': string,
    'price': number
}

const product = ref<ProductsType>()
const error = ref(null)

fetch("http://localhost:3000/products/" + route.params.id)
    .then((res) => res.json())
    .then((json) => (product.value = json))
    .catch((err) => (error.value = err))
</script>

<template>
    <h1>This is page product detail</h1>
    <div v-if="product">
        <h1>ID: {{ product.id }}</h1>
        <h3>Name: {{ product.name }}</h3>
        <p>Price: {{ product.price }} vnd</p>
    </div>
    <div v-else>Loading product {{ route.params.id }} ...</div>
</template>