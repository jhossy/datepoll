<script setup>
    import { defineProps } from 'vue';

    const props = defineProps({
        linkToPoll: String
    });
</script>

<template>
    <div class="container overflow-auto mw-75">
        <div class="row">
            <p>Link > <a :href="props.linkToPoll">{{ props.linkToPoll }}</a></p>
        </div>
    </div>
</template>