<template>
  <div>
    <div>
      <h1>Berikut adalah Tugas Pemrograman Web Lanjutan</h1>
    </div>
    <ul>
      <li v-for="item in todos" :key="item.id">{{item.deskripsi}} 
      <button @click="hapus(item.id)">Delete</button></li>
    </ul>
    <input v-model="myText" name="deskripsi"/>
    <button @click="tambah">Add</button>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  created: function() {
    axios.get('http://localhost:3000/todo')
    .then((result)=>{
      this.todos = result.data
    })
  },
  data : function() {
    return {
      todos : [],
      myText : '',
    }
  },
  methods : {
    tambah: function () { 
      let newItem = {deskripsi: this.myText} 
      axios.post('http://localhost:3000/todo', newItem)
      this.todos.push(newItem)
      this.myText= ""
    },
    hapus: function (id){
      axios.delete(`http://localhost:3000/todo/${id}`)
      location.reload()
    }
  }
}
</script>
