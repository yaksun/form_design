<template>
    <div id="show">
        
        <div 
           :item="item"
        >
            <span>{{item}}</span>
        </div>
    </div>
</template>
<script>
export default {
    props:{
        item:''
    },
  
}
</script>
<style lang="css">


    #show div{
        width:30px;
        height: 20px;
        background: red;
        margin: 20px 0;

    }
</style>