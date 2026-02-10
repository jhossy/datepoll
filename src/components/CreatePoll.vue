<script setup>
    import { computed, ref } from 'vue';

    const date = new Date().toISOString().slice(0, 16);
    const currentDate = ref(date);
    const selectedDates = ref([]);
    const isDisabled = computed(() => {
        return selectedDates.value.length > 9;
    });

    function doCreatePoll() {
        alert('Submitted poll with id: ' + crypto.randomUUID());
    }

    function doAddDate(){
        if(!selectedDates.value.includes(currentDate.value) && 
            !isDisabled.value) {
            selectedDates.value.push(currentDate.value);
        }
    }

    function doRemove(index) {
        selectedDates.value.splice(index, 1);
    }
</script>

<template>
    <div>
        <h1>Create Poll</h1>
        <div>
            <h2>1. Give it a name</h2>
            <input type="text" placeholder="Enter name here..." />
        </div>
        <div>
            <h2>2. Add dates & time</h2>
            <input type="datetime-local" v-model="currentDate" />
            <button @click="doAddDate" :disabled="isDisabled">Add date</button>
        </div>
        <div>
            <div v-for="(date, index) in selectedDates" :key="index">
                <span>
                    <input type="text" v-model="selectedDates[index]" />
                    <button @click="doRemove(index)">x</button>
                </span>
            </div>
        </div>
        <div>
            <h2>3. Create poll</h2>
            <button @click="doCreatePoll">Create poll</button>
        </div>
    </div>
</template>


