<script>
import { ref, reactive, onMounted, watch } from 'vue'
import FilterComp from '@/components/FilterMod.vue'

async function handlerGetter(page, name, status) {
    const url = `https://rickandmortyapi.com/api/character/?page=${page}&status=${status}`;
    let urlNew = url;
    if (name) {
        urlNew += `&name=${name}`;
    }
    try {
        let response = await fetch(urlNew)
        if (response.ok) {
            const data = await response.json()
            return data
        }
        //награмождения для исключения ошибки, когда сочетания букв в именах не нашлось
        else if (name) {
            response = await fetch(url)
            if (response.ok) {
                const data = await response.json()
                return data
            }
        } else {
            console.log('Ошибка при получении данных')
        }
    } catch (error) {
        console.log(error.message)
    }
}

export default {
    name: 'MainComp',
    components: { FilterComp },
    setup() {
        let loadInfo = reactive({ pages: 1 })
        let characters = ref([])
        let page = ref(1)
        let nameInput = ref('')
        let statusInput = ref('')
        const styleIndicator = (status) => {
            let color;
            switch (status) {
                case 'Alive':
                    color = 'green';
                    break;
                case 'Dead':
                    color = 'red';
                    break;
                default:
                    color = 'grey'
            }
            return { color };
        }
        const loadCharacters = async () => {
            const data = await handlerGetter(page.value, nameInput.value, statusInput.value);
            if (data && data.info) {
                loadInfo.pages = data.info.pages;
                characters.value = data.results;
            } else {
                characters.value = [];
            }
            console.log(data);
        }
        const handleSubmitForm = (values) => {
            nameInput.value = values.inputValueName;
            statusInput.value = values.inputValueStatus;
            page.value = 1
        }
        onMounted(loadCharacters)
        watch([page, nameInput, statusInput], loadCharacters)
        return {
            characters,
            loadInfo,
            page,
            styleIndicator,
            handleSubmitForm,
            nameInput,
            statusInput
        }
    },
}
</script>

<template>
    <div class="section">
        <FilterComp @submitForm="handleSubmitForm"></FilterComp>
        <ul class="wrapper">
            <div class="card" v-for="card in characters" :key="card.id">
                <div class="cardImage">
                    <img :src="card.image" alt="without img">
                </div>
                <div class="cardInfo">
                    <div class="cardInfo_item">
                        <h2 class="characterName"> {{card.name}}</h2>
                        <div class="characterStatus">
                            <p class="characterStatus_indicator" :style="styleIndicator(card.status)">&bull;&nbsp;</p>
                            <p>{{ card.status }} - {{ card.species }}</p>
                        </div>
                    </div>
                    <div class="cardInfo_item">
                        <h2 class="characterTitles">Last known location: </h2>
                        <p>{{ card.location.name }}</p>
                    </div>
                    <div class="cardInfo_item">
                        <h2 class="characterTitles">First seen in: </h2>
                        <p>{{ card.origin.name }}</p>
                    </div>
                </div>
            </div>
        </ul>
        <v-pagination class="small-pagination" :length=loadInfo.pages v-model="page" total-visible="6">
        </v-pagination>
    </div>
</template>

<style scoped lang="scss">
$base-color: white;
.section {
    background: rgb(39, 43, 51);
}

.wrapper {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    max-width: 1920px;
    padding: 20px 0;
    margin: 0 auto;
    gap: 30px;
    ul {
        list-style: none;
    }
}

.card {
    display: flex;
    width: 600px;
    height: 220px;
    border-radius: 8px;
    background: rgb(60, 62, 68);
    img {
        height: 100%;
        border-radius: 8px 0 0 8px;
    }
    .cardInfo {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        justify-content: space-between;
        color: $base-color;
        padding: 13.5px;
        font-size: 19px;
        .characterName {
            font-size: 26px;
        }
        .characterStatus {
            display: flex;
            flex-direction: row;
            align-items: center;
            justify-content: left;
            position: relative;
            &_indicator {
                color: green;
                font-weight: 900;
            }
        }
        .characterTitles {
            font-size: 16px;
            color: rgb(158, 158, 158);
        }
    }
}

.small-pagination {
    max-width: 50%;
    margin: 0 auto;
    color: white;
}
</style>