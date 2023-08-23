<script setup>
import { ref } from 'vue'
const Pathname = ref(window.location.pathname)
if (Pathname.value != "/") {
    document.title=Pathname.value + " - Noteonline"
}
</script>

<template>
    <span>{{ Pathname }}</span>
</template>