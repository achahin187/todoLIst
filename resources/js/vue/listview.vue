<template>
<div>
    <div v-for="(item,index) in items" :key="index" >
        <listitem :item="item" class="item" v-on:itemchanged="$emit('reloadlist')"></listitem>
    </div>
</div>

</template>


<script>
import listitem from "./listitem.vue"

export default {

    props:['items'],
    components:{
        listitem
    },

}
</script>

<style scoped>
.item {
background: #e6e6e6;
padding:5px;
margin-top: 5px;
}
</style>
