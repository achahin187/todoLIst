<template>
<div class="item">
      <input type="checkbox" @change="updateCheck()" v-model="item.completed"/>
   <span :class="[item.completed ? 'completed' : '','itemText']">   {{ item.name }}</span>
   <button @click="remove()" class="trashcan">
           <font-awesome-icon icon="trash" />

   </button>
</div>

</template>


<script>

export default {

props:['item'],

methods:{
    updateCheck(){
          axios.put('api/item/'+this.item.id,{
              item: this.item
        })
          .then((response) => {
             if(response.status == 200) {
                 this.$emit('itemchanged');
             }
          })
          .catch((err) => {
              console.error(err);
          })
    },
    remove(){
        axios.delete('api/item/'+this.item.id)
        .then((response) => {
              if(response.status == 200) {
                 this.$emit('itemchanged');
             }
        })
          .catch((err) => {
              console.error(err);
          })
    }
}

}
</script>

<style scoped>
.completed{
text-decoration: line-through;
color:#999999;

}
.itemText{
    width: 100%;
    margin-left: 20px;
}
.item{
    display:flex;
    justify-content: center;
    align-items: center;
}
.trashcan{
    color: red;
    border: none;
    background: #e6e6e6;
    outline: none;
}
</style>
