<script setup>
    function doCreatePoll() {
        alert('Submitted poll with id: ' + crypto.randomUUID());
    }
</script>

<template>
    <div>
        <h1>Create Poll</h1>
        <div>
            <h2>1. Give it a name</h2>
            <input type="text" placeholder="Enter name here..."><input>
        </div>
        <div>
            <h2>2. Select date & time</h2>
            <input type="datetime-local" />
        </div>
        <div>
            <h2>3. Create poll</h2>
            <button @click="doCreatePoll">Submit</button>
        </div>
    </div>
</template>


