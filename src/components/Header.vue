<script>
import { ref } from 'vue'

export default {
    name: 'HeaderComp',
    setup() {
        const links = ref(['Docs', 'About', 'Support'])
        return {
            links
        }
    }
}
</script>

<template>
    <header>
        <div class="headMenu">
            <div class="headLogo">
                <p>Logo</p>
            </div>
            <ul class="headLinks">
                <li v-for="item,index in links" :key="index">
                    <v-btn v-if="index==links.length-1" variant="outlined">
                        {{ item }}
                    </v-btn>
                    <v-btn v-else variant="plain">
                        {{ item }}
                    </v-btn>
                </li>
            </ul>
        </div>
        <div>
            <h1 class="headerTitle"> The Rick and Morty characters </h1>
        </div>
    </header>
</template>

<style lang="scss">
.headMenu {
    display: flex;
    justify-content: space-between;
    padding: 10px 5%;
    font-size: 30px;
    font-weight: 200;
}

.headLinks {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    gap: 10%;
    list-style: none;
    li a {
        text-decoration: none;
        color: black;
    }
}

.v-btn {
    text-transform: none;
}

.headerTitle {
    font-size: 5rem;
    padding: 8rem 0;
    font-weight: 900;
}
</style>
