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
    <div class="container">
        <form class="row g-2">
            <div class="row">
                <h1>Displaying poll: {{ $route.query.pid }}</h1>
            </div>
            <div class="row">            
                <ul v-for="(elm, index) in dateoptions" :key="index" class="list-group">
                    <li class="list-group-item">
                        <div class="col-auto form-check">
                            <label :for="'chk_' + index" class="form-label">{{ elm.date }}</label>
                            <input type="checkbox" :id="'chk_' + index" :value="elm.date" v-model="selectedDates" class="form-check-input"/>
                        </div>
                        <div class="col-auto">
                            <label for="staticVotes" class="visually-hidden" >Votes</label>
                            <input type="text" readonly class="form-control-plaintext" id="staticVotes" :value="elm.votes + 'votes'">
                        </div>
                    </li>
                </ul>
            </div>
            <div class="row g-2">
                <div class="col-auto">
                    <input type="text" placeholder="Enter name here..." v-model="userName" class="form-control"/>                
                </div>
                <div class="col-auto">
                    <button @click="btnSubmitVote" :disabled="userName.length === 0" class="btn btn-success mb-3">Submit vote</button>
                </div>
            </div>
        </form>
        {{ selectedDates }}
    </div>
</template>