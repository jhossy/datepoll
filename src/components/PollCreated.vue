<script setup>
    import { defineProps } from 'vue';

    const props = defineProps({
        linkToPoll: String
    });
</script>

<template>
    <div class="container overflow-auto mw-75">
        <div class="row">
            <p>
                <RouterLink :to="props.linkToPoll">{{ props.linkToPoll }}</RouterLink>
            </p>
        </div>
    </div>
</template>