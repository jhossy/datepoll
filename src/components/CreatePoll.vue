<script setup>
    import { computed, ref } from 'vue';
    import { defineEmits } from 'vue';
    // Declare the events this component can emit
    const emit = defineEmits(['poll-created']);

    const date = new Date().toISOString().slice(0, 16);
    const description = ref('');
    const currentDate = ref(date);
    const selectedDates = ref([]);
    const isAddDisabled = computed(() => {
        return selectedDates.value.length > 9;
    });
    const isCreateEnabled = computed(() => {
        return selectedDates.value.length > 0;
    });
    const isWarningHidden = ref(true);

    function doCreatePoll() {
        if(!isCreateEnabled.value)
            return;

        var pollCreated = {
            id: crypto.randomUUID(),
            dates: selectedDates.value,
            description: description.value
        };

        alert('Created poll: ' + JSON.stringify(pollCreated));
        emit('poll-created', JSON.stringify(pollCreated));
    }

    function doAddDate(){
        if(!selectedDates.value.includes(currentDate.value) && 
            !isAddDisabled.value) {
            isWarningHidden.value = true;
            selectedDates.value.push(currentDate.value);            
        } else{
            isWarningHidden.value = false;
        }
    }

    function doRemove(index) {
        selectedDates.value.splice(index, 1);
    }
</script>

<template>
    <div class="shadow p-3 mb-5 bg-body-tertiary rounded">
        <h1>New datepoll</h1>
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
                <button @click="doAddDate" :disabled="isAddDisabled" type="button" class="btn btn-success" aria-label="Add date">Add date</button>                
            </div>            
            <div class="mb-3">
                <span class="text-danger mx-2" :class="{ 'd-none' : isWarningHidden }" aria-label="Date already exists">
                    Date already exists
                </span>
                <div v-for="(date, index) in selectedDates" :key="index" class="list-group m-1">
                    <button @click="doRemove(index)" type="button" class="list-group-item list-group-item-action" title="Click to remove" aria-label="Click to remove">{{ new Date(date).toLocaleString() }}</button>
                </div>
            </div>            
        </div>
        <div class="mb-3">
            <label for="lbl-create-poll" class="form-label" aria-label="Create poll">3. Create poll</label>
            <div class="input-group">   
                <button @click="doCreatePoll" :disabled="!isCreateEnabled" type="button" class="btn btn-success">Create</button>
            </div>
        </div>
    </div>
</template>