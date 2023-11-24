<script setup lang="ts">
import { ref } from 'vue';
import { RouterLink } from 'vue-router'

interface ProductsType {
    'id': number,
    'name': string,
    'price': number
}

const products = ref<ProductsType[]>()
const error = ref(null)

fetch("http://localhost:3000/products")
    .then((res) => res.json())
    .then((json) => (products.value = json))
    .catch((err) => (error.value = err))
</script>

<template>
    <h1>This is page product list</h1>
    <div v-if="products?.length">
        <div class="item" v-for="product in products" :key="product.id">
            <RouterLink :to="{ name: 'product-detail', params: { id: product.id } }">{{ product.name }}</RouterLink>
            <div class="price">Price: {{ product.price }} vnd</div>
        </div>
    </div>
    <div v-else="products?.length">Loading Products ...</div>
</template>