<template>
<div>
    <Navigation @change-page="goToPage"/>
    
    <h1 class="title"> Ranking</h1>
    <img class="crown" src="../assets/Afbeelding1.png">
    <div class="podium">
        
            <div  class="podium2" v-for="(song,index) in sortsongs(songs).slice(1, 2)" :key="index" @songsort=(song,index)>
                    {{ song.points}} - {{ song.title }}
                    <br>
                    <iframe :src="song.spotify" width="100%" height="100%" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"></iframe>
            </div>
            
             <div class="podium1" v-for="(song,index) in sortsongs(songs).slice(0, 1)" :key="index" @songsort=(song,index)>
                    {{ song.points}} - {{ song.title }}
                    <br>
                    <iframe :src="song.spotify" width="100%" height="100%" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"></iframe>
            </div>
             <div class="podium3" v-for="(song,index) in sortsongs(songs).slice(2, 3)" :key="index" @songsort=(song,index)>
                    {{ song.points}} - {{ song.title }}
                    <br>
                    <iframe :src="song.spotify" width="100%" height="100%" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"></iframe>
            </div>
        
    </div>
    <br>
    <div class="allsongs">
      <div >
            <div class= "songs" v-for="(song,index) in sortsongs(songs).slice(3)" :key="index" @songsort=(song,index)>
                  
                <div class="number" > {{index+4}} </div> 
                {{ song.points}} - {{ song.title }}
                <br>
                <iframe  :src="song.spotify" width="90%" height="80px" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"></iframe>
          
          </div>
        </div>
    </div>


</div>

</template>

<script>
import Navigation from "..//components/Navigation.vue"
export default {
    name:"Rankingpage",
    components: {
        Navigation
    },
    data(){
        return{
            songs:[],
            ids:[]
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
            .then((songs)=> {
                this.fetchPoints(songs);
            })

        },
        fetchPoints(songs){
            console.log(songs)
            songs.map((song) => {
                song.points = 0;
                return song;
            })

            // get points from each song
            songs.forEach((song, index) => {

                const id=song.id;;

                const url="http://webservies.be/eurosong/Songs/" + id +"/points";
            fetch(url)
            .then((response)=> {
                return response.json();
            })
            .then((points)=> {
                songs[index].points=points;
            })

                //console.log(songs)
            })

           this.songs = songs;

            //console.log(songs);
        },
        sortsongs(songs) {
            console.log("test")
            return this.songs.slice().sort((a, b) => b.points - a.points );
        // Set slice() to avoid to generate an infinite loop!
}
    }

    }


</script>