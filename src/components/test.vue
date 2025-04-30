<script setup>
    import {ref,reactive,computed} from 'vue';
    const people = reactive([
        {name:"nicole", icon:"123.jpg", big:false, small:false},
        {name:"jack", icon:"456.jpg", big:false, small:false}
    ])
    const update=(person)=>computed(()=>{
        if(person.big)
            console("big changed!");
        else if(person.small)
            console("small changed!");
        else
            console("nothing happend");
    })
</script>

<template>
    <div v-for="person in people" :key="person.name" v-if="update(person)">
        <p>{{ person.name }}</p>
        <label>
            <input type="checkbox" v-model="person.big">大
            {{ person.big }}
        </label>
        <label>
            <input type="checkbox" v-model="person.small">小
            {{ person.small }}
        </label>
    </div>
    <hr>
    <h3>目前:{{people}}</h3>
</template>

<style>

</style>