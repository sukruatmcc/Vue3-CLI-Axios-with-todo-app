<template>
  <div class="container">
    <h3 class="text-center text-red">Todo App</h3>
     <AddSection @add-section-list="onSave"/>
    <ul v-if="this.itemList.length > 0">
     <ListSection :itemList="itemList" @on-delete="onDelete($event)"/>
    </ul>
    <div v-else class="bg-red text-white p-3">
      Not Found...
    </div>
    <ResultBar :itemList="itemList"/>
  </div>
</template>
<script>
import axios from "axios"
import ListSection from "@/components/ListSection";
import ResultBar from "@/components/ResultBar";
import AddSection from "@/components/AddSection";
export default {
  components: {AddSection, ResultBar, ListSection},
  data(){
    return{
      itemList:[]
    }
  },
  mounted(){
     axios.get('http://localhost:3000/posts').then(items_response => {
       console.log(items_response);
       this.itemList = items_response.data || [];
     });
  },
  methods:{
    onSave(event){
      const saveObject = {
        id:new Date().getTime(),
        title:event.target.value,
        completed: false
      };
      axios.post('http://localhost:3000/posts',saveObject).then(save_response => {
        console.log(save_response)
        this.itemList.push(save_response.data)
        event.target.value="";
        event.target.focus()
      });
    },
    onDelete(item){
      axios.delete(`http://localhost:3000/posts/${item.id}`).then(delete_response => {
        console.log(delete_response);
        this.itemList =  this.itemList.filter(i => i !== item)
      });
    }
  }
}
</script>
