<template>
    <div> 
     <img class="crown" src="../assets/Afbeelding1.png">
    <div class="podium">
        
            <div  class="podium2" v-for="(song,index) in sortsongs(items).slice(1, 2)" :key="index" @songsort=(song,index)>
                    {{ song.points}} - {{ song.title }}
                    <br>
                    <iframe :src="song.spotify" width="100%" height="100%" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"></iframe>
            </div>
            
             <div class="podium1" v-for="(song,index) in sortsongs(items).slice(0, 1)" :key="index" @songsort=(song,index)>
                    {{ song.points}} - {{ song.title }}
                    <br>
                    <iframe :src="song.spotify" width="100%" height="100%" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"></iframe>
            </div>
             <div class="podium3" v-for="(song,index) in sortsongs(items).slice(2, 3)" :key="index" @songsort=(song,index)>
                    {{ song.points}} - {{ song.title }}
                    <br>
                    <iframe :src="song.spotify" width="100%" height="100%" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"></iframe>
            </div>
        
    </div>
      
    </div>
</template>

<script>
    export default {
        name: "Podium",
        props: [
            "items",
        ],
        methods:{
            sortsongs(items) {
                // console.log("test")
                return this.items.slice().sort((a, b) => b.points - a.points );
        // Set slice() to avoid to generate an infinite loop!
        }
        }
    }
</script>
