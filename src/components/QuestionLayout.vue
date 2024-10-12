<script setup>
    defineProps(
        {
            question: String
        }
    )
</script>

<template>
    <div>
        <h3>{{ question }}</h3>
        <div v-if="$slots.questions">
            <slot name="questions"></slot>
        </div>
    </div>
</template>

<style>
    
</style>