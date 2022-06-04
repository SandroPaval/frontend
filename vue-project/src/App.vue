<template>
  <header>
    <button class="sideBar">sidebar</button>
      <router-link class="link" to="/">
          <h1 class="PageName"><span>Mac</span>Gillis<span>Club</span></h1>
      </router-link>
       <form @submit.prevent="SearchAnimes()" class="search-box">
              <input type="text" placeholder="What are you looking for?" v-model="search" />
              <input type="submit" value="Search"/>
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
  font-un

  &::selection{
    background: transparentize(#42B883,0.5)
  }
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


.cardsSet {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
}

header{
  display: inline-block;
  min-width: 100%;
  justify-content: start;
  padding: 10px 16px;
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