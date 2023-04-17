<template>
    <div>
        <h1>Sobre</h1>

        <p v-if="author"> author: {{ author }} </p>
        <input type="text" v-model="author">

    </div>
</template>

<script>
export default{
    name:'SobreVue',
    data(){
        return {
            author:''
        }
    },
    created(){
        console.log('Created Sobre...')
    },
    destroyed(){
        console.log('Destroyed Sobre...')
    },
    activated(){
        console.log('Activated Sobre...')
    },
    deactivated(){
        console.log('Deactivated Sobre...')
    }
}
</script>