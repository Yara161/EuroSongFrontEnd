<template>
    <div v-if="isvisible" v-bind:data-count="count">
        Buttoncounter: {{count}}

        <button @click="addOne()">
            Add 1
        </button>

         <button @click="minOne()">
            Min 1
        </button>
          <button @click="hide()">
            Hide
        </button>
    </div>
</template>
<script>
export default{
    name:"Counter",
    data() {
        return {
            count:10,
            isvisible:true
        }
    },
    methods:{
        addOne(){
            this.count++;
        },
        minOne(){
            this.count--;
        },
        hide(){
            this.isvisible=false
        }
    }
}
</script>
