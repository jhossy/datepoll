<script setup>
    import { computed, readonly, ref } from 'vue';

    const date = new Date().toISOString().slice(0, 16);
    const description = ref('');
    const currentDate = ref(date);
    const selectedDates = ref([]);
    const isDisabled = computed(() => {
        return selectedDates.value.length > 9;
    });

    function doCreatePoll() {
        var pollCreated = {
            id: crypto.randomUUID(),
            dates: selectedDates.value,
            description: description.value
        };

        alert('Created poll: ' + JSON.stringify(pollCreated));
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
    <div class="shadow p-3 mb-5 bg-body-tertiary rounded">
        <h1>Create new datepoll</h1>
        <div class="mb-3">
            <label for="lbl-enter-name" class="form-label" aria-label="Give it a name">1. Give it a name</label>
            <div class="input-group">                
                <input v-model="description" id="lbl-enter-name" class="form-control" type="text" placeholder="Enter name here..." aria-label="Enter name here..."/>
            </div>
        </div>
        <div class="mb-3">
            <label for="lbl-add-date-and-time" class="form-label" aria-label="Add dates & time">2. Add dates & time</label>
            <div class="input-group">                
                <input v-model="currentDate" id="lbl-add-date-and-time" class="form-control mx-1" type="datetime-local" aria-label="Current date"/>
                <button @click="doAddDate" :disabled="isDisabled" type="button" class="btn btn-success" aria-label="Add date">Add date</button>
                <div v-for="(date, index) in selectedDates" :key="index" class="input-group">
                    <div class="input-group">
                         <input :value="new Date(date).toLocaleString()" disabled type="text" class="form-control m-1" />
                        <button @click="doRemove(index)" type="button" class="btn btn-danger m-1">x</button>                        
                    </div>
                </div>
            </div>            
        </div>
        <div class="mb-3">
            <label for="lbl-create-poll" class="form-label" aria-label="Create poll">3. Create poll</label>
            <div class="input-group">   
                <button @click="doCreatePoll" type="button" class="btn btn-success">Create poll</button>
            </div>
        </div>
    </div>
</template>


