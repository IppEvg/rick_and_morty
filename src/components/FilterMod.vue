<script>
import { ref } from 'vue';
export default {
    name: 'FilterComp',
    setup(_,{ emit }) {
        const inputValueName = ref('');
        const inputValueStatus = ref('');
        const submitForm = () => {
        emit('submitForm', { inputValueName: inputValueName.value, inputValueStatus: inputValueStatus.value })
    }
        return{
            inputValueName,
            inputValueStatus,
            submitForm
        }
    }
}
</script>

<template>
    <div class="wrapperFilters">
        <form class="inputs" @submit.prevent="submitForm">
            <v-text-field label="Name" max-width="30%" v-model="inputValueName"></v-text-field>
            <v-select
                label="Status"
                :items="['','Alive', 'Dead', 'unknown']"
                v-model="inputValueStatus"
            ></v-select>
            <v-btn class="btnFilters" type="submit">APPLY FILTERS</v-btn>
        </form>
    </div>
</template>
<style scoped >
.wrapperFilters{
    max-width: 40%;
    padding-top: 20px;
}
h1{
    color: white;
    padding-top: 10px;
}
.inputs{
    color: white;
    display: flex;
    flex-direction: row;
    align-items:center ;
    justify-content: center;
    gap: 5%;
    height: fit-content;
}

</style>