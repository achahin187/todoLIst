<template>
    <div class="todoListContainer">
        <div class="heading">

            <h2 id="title">Todo List</h2>
            <additemform v-on:reloadlist="getList()" />
        </div>
        <listview :items="items" v-on:reloadlist="getList()"/>
    </div>
</template>


<script>
import additemform from './additemform'
import listview    from './listview'

export default {
    components:{
        additemform,
        listview
    },
    data:function(){
        return {
            items:[]
        }
    },
    methods:{
        getList(){
            axios.get('api/items')
            .then((response) => {
                this.items = response.data
            })
            .catch((err) => {
                console.error(err)
            })
        }
    },
    created(){
       this.getList();
    }

}
</script>

<style scoped>
.todoListContainer{
    width:350px;
    margin:auto;
}
.heading{
    background: #e6e6e6;
    padding:10px;
}
#title{
    text-align:center;
}



</style>

