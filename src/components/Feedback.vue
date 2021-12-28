<template>
    <div :class="'c-feedback ' + classType" v-if="isactive" @click="hide()">
        {{message}}
        {{classType}}
    </div>
</template>
<script>
export default {
    name: "Feedback",
    data(){
        return{
            isactive:true
        }
    },
    props:[
        'message',
        'classType'
    ],
    methods:{
        hide(){
            this.isactive=false
        }
    }
}
</script>