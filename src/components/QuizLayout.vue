<script setup>
    defineProps(
        {
            title: String
        }
    )
</script>

<template>
    <div >
        <h1>{{ title }}</h1>
        <div v-if="$slots.container">
            <slot name="container">
            
            </slot>
        </div>
    </div>
</template>

<style scoped>
    
</style>