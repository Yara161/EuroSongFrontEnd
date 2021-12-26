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
  
        <h1 class="title"> Game </h1>

        <!-- <div v-for="song in songs" :key=song.id>
            {{song.artist.name}} - {{song.title}}
        </div> -->

        <Carousel 
            :items="songs"
            :activeIndex="activeSongIndex"
            @change-index="changeActiveSongIndex"
        />

    <div class="pointsbuttons">
        <div class="points" v-for="(vote,index) in votes" :key="index">
            <button class="buttonpoints"  @click="AddVote(vote.points)" v-if="!vote.isVoted">
            Add {{vote.points}} points
            {{vote.isVoted}}
            </button>
        </div>
    </div>
  </div>
</template>
<script>


//components
import Carousel from "..//components/Carousel.vue"
import Navigation from "..//components/Navigation.vue"

export default {
    name:"Gamepage",
    components: {
        Carousel,
        Navigation
    },
    data(){
        return{ 
            songs:[],
            activeSongIndex:0,
            votes: [
                {
                    points:1,
                    isVoted:false
                },
                {
                    points:2,
                    isVoted:false
                },
                {
                    points:3,
                    isVoted:false
                },
                {
                    points:4,
                    isVoted:false
                },
                {
                    points:8,
                    isVoted:false
                }
            ]
        }
    },
    mounted(){
        console.log("mounted");
        //Get all songs
       this.fetchSongs();
    },
    methods:{
        //navigation method
        goToPage(page){
            this.$emit("change-page",page);
        },
        //data method
        fetchSongs(){
            const url ="http://webservies.be/eurosong/Songs";

            fetch(url)
            .then((response)=> {
                return response.json();
            })
            .then((songs)=> {
                this.fetchArtists(songs);
            });
        },

        postVote(points) {
                const songId = this.songs[this.activeSongIndex].id;
                const url = "http://webservies.be/eurosong/Votes";
                fetch(url, {
                    method: "POST",
                    headers: {
                        'Accept': 'application/json, text/plain',
                        'Content-Type': 'application/json;charset=UTF-8'
                    },
                    body: JSON.stringify({
                        songID: songId,
                        points: points,
                    })
                }).then((response) => {
                    return response.json();
                }).then((result) => {
                    console.log(result);
                })
            },

        fetchArtists(songs){
             const url ="http://webservies.be/eurosong/Artists";

            fetch(url)
            .then((response)=> {
                return response.json();
            })
            .then((artists)=> {
                //loop over array songs with forEach method
                console.log(songs);
                //find the artist in an array
                songs.map((song) => {
                    const artist=artists.find((artist)=> artist.id == song.artist);

                    //replace the id by the artist object
                    song.artist=artist;

                    //return the new object
                    return song;
                });   

                //change data of songs so everything will get rerenderd
                this.songs=songs;
            });
        },
        changeActiveSongIndex(index){
            this.activeSongIndex=index;
        },

        AddVote(points){
            //copy
            let votes= this.votes;
            //create new array when points is equel to given points, change isVoted state so it dissepears
            votes.map((vote) => {
                if (vote.points == points)
                {
                    vote.isVoted=true;
                }
                return vote
            });

            //post it to the api
            this.postVote(points);

            //check if all votes isVOted are set to true OR there are nog false votes
            let activeVotes = votes.filter((vote)=> vote.isVoted==true);
            
            if(activeVotes==activeVotes.length)
            {
                this.goToPage("ranking");
            }
        }

    }
}
</script>
