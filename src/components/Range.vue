<script setup>
    defineProps(
        {
            val: Number
        }
    )
</script>

<template>
    <div>
        <input type="range" name="" id="" :value="val" disabled>
        <slot>
            
        </slot>%
    </div>
</template>

<style scoped>
    
</style>