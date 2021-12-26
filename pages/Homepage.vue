<template>
    <div>
          <div class="navbar">
            <button class="navbar button" @click="goToPage('home')">
                Home
            </button>
            <button class="navbar button" @click="goToPage('game')">
                    Game
            </button>
            <button class="navbar button active"   @click="goToPage('ranking')">
                Ranking
            </button>
        </div>
  
        <h1 class="title"> Eurosong voting app </h1>
        <h2 class="title2">
           Total songs: {{songs.length}}
        </h2>
    </div>
</template>
<script>

export default {
    name:"Homepage",
    data(){
        return{ 
            songs:[]
        }
    },
    mounted(){
        console.log("mounted");
        //Get all songs
       this.fetchSongs();
    },
    methods:{
        goToPage(page){
            this.$emit("change-page",page);
        },
    fetchSongs(){
           //get alle the songs
            const url ="http://webservies.be/eurosong/Songs";

            fetch(url)
            .then((response)=> {
                return response.json();
            })
            .then((songs)=>
            {
               this.songs=songs;
            console.log(songs);
            }) 
        }
        }}

    
</script>
