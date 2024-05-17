<script>
import { ref } from 'vue'

export default {
    name: 'FooterMod',
    setup() {
        const icons = ref([
            'mdi-facebook',
            'mdi-twitter',
            'mdi-linkedin',
            'mdi-instagram',
        ])
        return { icons }
    }
};
</script>

<template>
    <v-footer class="d-flex flex-column">
        <div class="stringFirst d-flex w-100 align-center px-4">
            <strong>CHARACTERS: 826</strong>
            <strong>LOCATIONS: 126</strong>
            <strong>EPISODES: 51</strong>
            <v-spacer></v-spacer>
            <div>
                <v-btn v-for="icon in icons" :key="icon" :icon="icon" class="mx-4 icons" size="small" variant="plain"></v-btn>
            </div>
        </div>
        <div class="down px-4 py-2 text-center w-100">
            ❮❯ by Axel Fuhrmann 2024
        </div>
    </v-footer>
</template>
  
<style scoped>
footer {
    padding: 0;
}

.d-flex {
    display: flex;
}

.flex-column {
    flex-direction: column;
}

.stringFirst {
    background-color: rgb(32, 35, 41);
    color: white;
    display: flex;
    flex-direction: column;
    padding-top: 40px;
}

.bg-black {
    background-color: black;
    color: white;
}

.w-100 {
    width: 100%;
}

.align-center {
    align-items: center;
}

.px-4 {
    padding-left: 1rem;
    padding-right: 1rem;
}

.py-2 {
    padding-top: 0.5rem;
    padding-bottom: 0.5rem;
}

.text-center {
    text-align: center;
}

.icons {
    margin-top: 10px;
}

.down {
    background-color: rgb(32, 35, 41);
    ;
    color: white;
}
</style>