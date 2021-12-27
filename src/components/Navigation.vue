<template>
  <div id="navbar">
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
  </div>
</template>
<script>
    export default {
        name: "Navigation",
    methods:{
        //navigation method
        goToPage(page){
            this.$emit("change-page",page);
        }
    }
    }
</script>