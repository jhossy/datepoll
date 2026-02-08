<script setup>
    import { ref } from 'vue';

    const date = new Date().toISOString().slice(0, 16);
    const currentDate = ref(date);
    const selectedDates = ref([]);

    function doCreatePoll() {
        alert('Submitted poll with id: ' + crypto.randomUUID());
    }

    function doAddDate(){
        if(!selectedDates.value.includes(currentDate.value)) {
            selectedDates.value.push(currentDate.value);
            console.log('added - ' + currentDate.value);
        }
        //alert('Clicked add date with ' + currentDate.value);
        for(var i = 0; i < selectedDates.length; i++){
            console.log(selectedDates[i].value);
        }
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
            <button @click="doAddDate">Add date</button>
        </div>
        <div>
            <div v-for="(date, index) in selectedDates">
                <input type="text" key="index" v-model="selectedDates[index]" />
            </div>
        </div>
        <div>
            <h2>3. Create poll</h2>
            <button @click="doCreatePoll">Create poll</button>
        </div>
    </div>
</template>


