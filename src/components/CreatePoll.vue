<script setup>
    import { ref } from 'vue';

    const date = new Date().toISOString().slice(0, 16);
    const currentDate = ref(date);
    var selectedDates = [];

    function doCreatePoll() {
        alert('Submitted poll with id: ' + crypto.randomUUID());
    }

    function doAddDate(){
        selectedDates.push(currentDate);
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
            <h2>3. Create poll</h2>
            <button @click="doCreatePoll">Create poll</button>
        </div>
    </div>
</template>


