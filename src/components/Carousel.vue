<template>
    <div>
       
       
    <div class="songsgame">
         <img  @click="changeIndex(-1)" class="arrow" src="../assets/arrowleft.png">

        <div  v-for="(song,index) in items" :key="song.id">
            <div class="song" v-if="index == activeIndex">

            {{ song.artist.name}} - {{ song.title }}
            <iframe   :src="song.spotify" width="100%" height="100%" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"></iframe>
            </div>
        </div> 
        <img  @click="changeIndex(+1)" class="arrow" src="../assets/arrowright.png"> 

    </div>

      
    </div>
</template>

<script>
    export default {
        name: "Carousel",
        props: [
            "items",
            "activeIndex"
        ],
        methods:{
            changeIndex(value) {
                //copy, you cannot change props directly
                let index = this.activeIndex;

                //-1 of 1

                index +=value;
                //check if index is the beginning or ending
                if (index<0){
                    index= this.items.length-1;
                }

                else if( index == this.items.length)
                {
                    index=0;
                }
                //change index
                this.$emit("change-index", index);               
                console.log(index);
            }
        }
    }
</script>
