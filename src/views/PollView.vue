<script setup>
    import { ref } from 'vue';
    const date1 = new Date().toISOString().slice(0, 16);
    const date2 = new Date('2026-01-21T15:31').toISOString().slice(0, 16);
    const date3 = new Date('2026-03-21T15:31').toISOString().slice(0, 16);

    const dateoptions = [{date : date1, votes: 1}, {date : date2, votes: 2}, { date: date3, votes: 1}];
    const selectedDates = ref([]);
    const userName  = ref('');

    function btnSubmitVote() {
        alert(userName.value + ' submitted vote: ' + selectedDates.value.length);
    }
</script>

<template>
    {{ $route.query.pid }}
    <div class="container shadow p-3 mb-5 bg-body-tertiary rounded">
        <h1>Please vote</h1>
        <div class="row">
            <form >
                <div class="col">            
                    <ul class="list-group">
                        <li v-for="(elm, index) in dateoptions" :key="index" class="list-group-item d-flex justify-content-between">                            
                            <div>
                                <label :for="'chk_' + index" class="form-label">{{ elm.date }}</label>
                                <small class="text-muted mx-3">{{ elm.votes }} votes</small>
                            </div>
                            <input type="checkbox" :id="'chk_' + index" :value="elm.date" v-model="selectedDates" class="form-check-input"/>
                        </li>
                    </ul>
                </div>
                <hr />
                <div class="col">
                    <div class="col-auto">
                        <input type="text" placeholder="Enter your name here..." v-model="userName" class="form-control"/>                
                    </div>
                    <div class="col-auto mt-2 d-flex justify-content-end">
                        <button @click="btnSubmitVote" :disabled="userName.length === 0" class="btn btn-success mb-3">Submit vote</button>
                    </div>
                </div>
            </form>
        </div>
        {{ selectedDates }}
    </div>
</template>