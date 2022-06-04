<template>
   <div class="card">  
                <img class="image"
                        :src="anime.images.jpg.large_image_url"
                        :alt="anime.title + ' Poster'"
                        />
                            <div class="textBox">
                                <a :href="anime.url">
                                    <h2 class="title" >{{anime.title}}</h2> 
                                </a>
                                    <div class="descriptionBox">
                                        <h3 class="description">rating: {{anime.score}}</h3>
                                        <h3 class="description">episodes: {{anime.episodes}} </h3>
                                        <h3 class="description">from: {{anime.season}} {{anime.year}}</h3>
                                        <h3 class="description">genre:  {{anime.genres[0].name}}  </h3>

                                </div>
                            </div>  


   </div> 
</template>

<script>
export default {
    props: ['anime']
}
</script>

<style>
.card{
width: 250px;
margin-left: 15px;
margin-top: 15px;
background: rgb(17, 16, 16);
border-radius: 20px;
position: relative;
}

.image{
    border-top-left-radius: 20px;
    border-top-right-radius: 20px;
    border-bottom-color: white;
    border-bottom-width: 5px;
    width: 100%;
    height: 300px;
}

.textBox{
    height: 200px;
    margin: 2%;
    margin-top: -1%;
}

.descriptionBox{
    height:105px;
    width:97%;
    position: absolute;
    bottom: 0;
    

    
}

.title{
color:white;
height: 95px;
font-size: 26px;
overflow-wrap: break-word;
overflow:auto
}

.title::-webkit-scrollbar{
background-color: rgb(17, 16, 16) 
}

.title::-webkit-scrollbar-thumb{
    background-color:rgb(65, 70, 70);
    border-radius: 20px;
    border: 3px solid white;
}

.description{
    color:white;
}

</style>