<script setup lang="ts">
import { RouterLink } from 'vue-router'
</script>

<template>
    <nav>
        <RouterLink :to="{ name: 'home' }">Home</RouterLink>
        <RouterLink :to="{ name: 'about' }">About</RouterLink>
        <RouterLink :to="{ name: 'product' }">Product</RouterLink>
    </nav>
</template>