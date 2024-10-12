<script setup>
    import { ref } from 'vue';

    const active = ref(false)
    const props = defineProps(
        {
            content: String,
            click: Boolean
        }
    )

    console.log(props.click);

</script>

<template>
    <div>
        <input type="submit" :value="content" :disabled="!active"> {{ active }}
    </div>
</template>

<style scoped>
    
</style>