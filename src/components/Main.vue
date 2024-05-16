<template >
    <div >
        <ul class="wrapper">
                <div class="card" v-for="card in characters" :key="card.id">
                    <div class="cardImage">
                        <img :src="card.image" alt="without img">
                    </div>
                    <div class="cardInfo">
                        <div class="cardInfo_item">
                            <h2 class="characterName"> {{card.name}}</h2>
                            <div class="characterStatus"><p class="characterStatus_indicator" :style="styleIndicator(card.status)">&bull;&nbsp;</p><p>{{ card.status }} - {{ card.species }}</p></div>
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
    </div>
</template>
<script>
import { ref, onMounted} from 'vue';

    async function handlerGetter(){
    let response = await fetch('https://rickandmortyapi.com/api/character')
    if (response.ok) {
            const data = await response.json()
            return data.results
          }else{
            console.log('Ошибка при получении данных')
            return
          }
}
export default{
    name:'MainComp',
    setup(){
        let characters = ref([])
        const styleIndicator = (status) => {
      let color;
      switch (status) {
        case 'Alive':
          color = 'green';
          break;
        case 'unknown':
          color = 'grey';
          break;
        case 'Dead':
          color = 'red';
          break;
          default:
            color='grey'
      }
      return { color };
    }
        onMounted(async() => {
            characters.value = await handlerGetter()
            console.log(characters);
        })
        
         return {
        characters,
        styleIndicator
        }
    },
   
}
</script>

<style scoped lang="scss">
$base-color: white;
.wrapper{
    background: rgb(39, 43, 51);
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    max-width: 1920px;
    gap: 30px;
    ul{
        list-style: none;
    }
}
.card{
display: flex;
width: 600px;
height: 220px;
border: 1px solid red($color: #000000);
border-radius: 20px;

    img{
        height: 100%;
    }
    .cardInfo{
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        justify-content: space-between;
        color: $base-color;
        padding: 13.5px;
        font-size: 19px;
        .characterName{
            font-size: 26px;
        } 
        .characterStatus{
            display: flex;
            flex-direction: row;
            align-items: center;
            justify-content: left;
            position: relative;
            &_indicator{
                color: green;
                font-weight: 900;
            }
        }
        .characterTitles{
            font-size: 16px;
            color:rgb(158, 158, 158);
        }
    }
}

</style>