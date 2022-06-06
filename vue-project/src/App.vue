<template>
  <header>
    <button class="sideBar">sidebar</button>
      <router-link class="link" to="/">
          <h1 class="PageName"><span>Mac</span>Gillis<span>Club</span></h1>
      </router-link>
       <form @submit.prevent="SearchAnimes()" class="search-box">
              <input type="text" placeholder="What are you looking for?" v-model="search" class="search-field" />
              <input type="submit" value="Search" class="search-button" />
            </form>
  </header>
  <main>
            <div class="cardsSet" v-if="animes.length > 0">
              <AnimeCard
                          v-for="anime in animes"
                          :key="anime.mal_id"
                          :anime="anime"/>
            </div>
    <router-view/>
  </main>
</template>

<script>
import {ref} from 'vue';
import AnimeCard from './components/AnimeCard.vue'

export default {
    components: {
        AnimeCard,
        },
setup() {
  const search = ref('');
  const animes = ref([]);

    const SearchAnimes = async () => {
     const url = `https://api.jikan.moe/v4/anime?q=${search.value}&sfw`
     fetch(url)
          .then(res => res.json())
          .then(res => {
            animes.value =  res.data
          })
    console.log(animes.value)
    }

    return {
      AnimeCard,
      search,
      animes,
      SearchAnimes
    }
}
}

</script>

<style lang="scss">
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans', sans-serif; 
}

body {
  background-color: #687079;
}

a {
  text-decoration: none;
}

.sideBar {
  max-width: 15%;
  margin-left: 3.5%;

}

.search-box {
  background-color: #235392;
  width:max-content;
  height: 180%;
  width: 100%;
  border-radius: 20px;
}

.search-field{
height:100%;
width:80%;
border: solid;
border-right: none;
border-top-left-radius: 20px;
border-bottom-left-radius: 20px;
border-color: #235392;
border-width: 8px;
color: #235392;
font-size: 15px;
font-weight: bold;
font-family: 'Fira Sans', sans-serif;
padding: 1px;
}

.search-button{
height: 90%;
width: 20%;
border: solid;
border-top-right-radius: 20px;
border-bottom-right-radius: 20px;
border-color: #235392;
border-width: 5px;
background-color: #235392;
color: white;
font-size: 15px;
font-weight: bold;
font-family: 'Fira Sans', sans-serif; 
}

.search-button:hover {
background:white;
color: #235392;
cursor: pointer;
}

.search-button:active {
background-color: #235392;
border-color: #235392;
color: white;
}


.cardsSet {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
}

header{
  display: grid;
  grid-template-columns:auto;
  min-width: 100%;
  justify-content: start;
  padding: 1% 1%;
  background-color: #1a232c;
  box-shadow: 0px 0px 6px rgba(0,0,0,0.1);
  
}

h1{
  color: #FFF;
  font-size: 500%;
  text-shadow: 3px 3px 3px  #060a0f;

    span{
      color: #235392;
    }
}


</style>