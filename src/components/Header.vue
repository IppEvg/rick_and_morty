
<template >
    <header>
        <div class="headMenu">
            <div class="headLogo">
                <p>Logo</p>
            </div>
            <ul class="headLinks">
                <li v-for="item in links" :key="item" ><a href="#">{{ item }}</a></li>
            </ul>
        </div> 
        <div>
            <h1 class="headerTitle"> The Rick and Morty characters </h1>
        </div>
    </header>
</template>
<script>
import { ref } from 'vue'

export default{
    name:'HeaderComp',
    setup(){
        const links = ref(['Docs','About','Support'])
        
         return {
        links
        }
    }
}
</script>

<style lang="scss">
.headMenu{
display: flex;
justify-content: space-between;
padding: 0 5%;
font-size: 30px;
font-weight: 600;
}
.headLinks{
display: flex;
flex-direction: row;
align-items: center;
justify-content: center;

gap: 10%;
list-style: none;
li a{
  text-decoration: none;  
  color:black;
}
}
.headerTitle{
    font-size: 5rem;
}
</style>
