<template>
    <div>
        <h1>propes</h1>
        <p>{{name}}</p>
        
        <p v-for=" data in arydata" :key="data.name">{{data.name}}--{{data.lname}}</p>
    </div>
</template>
<script>
export default({    
    name:'props',
    props:["name","arydata"]
})
</script>
