<template>
    <div>
       
        <button @click="changeIndex(-1)">
            Prev song
        </button>

        <div v-for="(song,index) in items" :key="song.id">
            <div v-if="index == activeIndex">

            {{ song.artist.name}} - {{ song.title }}
            <iframe :src="song.spotify" width="100%" height="50%" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"></iframe>
            </div>
        </div>

        <button @click="changeIndex(+1)">
            Next song
        </button>
    </div>
</template>

<script>
    export default {
        name: "Top3Songs",
        props: [
            "items",
            
        ],
        methods:{
           
        }
    }
</script>
