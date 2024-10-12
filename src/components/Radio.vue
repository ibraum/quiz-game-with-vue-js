<script setup>
    defineProps(
        {
            label: String,
            nameValue: String,
            value: String,
            k: String
        }
    )

    const model = defineModel()
</script>

<template>
    <div>
        <input type="radio" :name="nameValue" v-model="model" :value="value" :key="k" :checked="false">
        <span>{{ label }}</span>
    </div>
</template>

<style>
    
</style>