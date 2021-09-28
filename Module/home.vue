// conditional rendering

<template>
    <div>
        <h1 v-if="show">Conditional Rendering</h1>
        <!-- <h1 v-else>else side</h1> -->
        <button v-on:click="display">toggle</button>
    
    </div>
</template>

<script>


export default{
    name:'home',
    props: {
        data : String,
        msg : String
    }, data()
    {
        return {
            show:false
        }
    },
    methods:{
        display()
        {
            this.show= true
        }
    }
    }
    

</script>

