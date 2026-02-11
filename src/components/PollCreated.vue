<script setup>
    const props = defineProps({
        linkToPoll: String
    });
</script>

<template>
    <div class="container">
        <div class="row">
            <h2>Link to poll > <a :href="props.linkToPoll">{{ props.linkToPoll }}</a></h2>
        </div>
    </div>
</template>