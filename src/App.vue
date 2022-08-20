<template>
<div>
  <h1>Simple TO-DO APP (LOCAL STORAGE)</h1>
  <div class="inputs">
  <input type="text" placeholder="Enter task" v-model="this.val"> 
  <button @click="addToStorage">Add</button>
  <button @click="clear">Clear All</button>
  </div>
  <div  class="tasks" v-for="task in List" :key="task">{{ task }}

    <button @click="Delete(task)">Delete</button>
  </div>
</div>
</template>

<script>

export default {
data() {
    return {
        List : [],
        val : ''
    }
},
 mounted() {
    if (localStorage.tasks) {
      this.List = JSON.parse(localStorage.tasks);

    }
 },
methods : {
 addToStorage() {
    this.List.push(this.val)
    this.val=""
    localStorage.tasks = JSON.stringify(this.List)
 },
 Delete(key) {

    this.List = this.List.filter((x) => x != key)
    
   
 },
 clear() {
    this.List = []
    localStorage.clear()
 }

},
 watch: {
    List(newVal) {
        localStorage.tasks = JSON.stringify(newVal)
    }
 }
}
</script>

<style scoped>
.tasks {
    padding: 20px;
    background-color: #eee;
    border: 1px solid black;
    margin-top:5px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.inputs {
    background-color: rgb(228, 80, 80);
    color: white;
    padding: 20px;
    display: flex;
    justify-content: center;
}
button {
    padding: 10px 20px;
    background: rgb(121, 11, 11);
    color:white;
    margin-right: 5px;
    transition: 0.3s ease-in;
}
button:hover {
    color:rgb(121, 11, 11);
    background: white;
    
}
input:focus {
outline: none;
}
input {
    width: 300px;
    border: none;
}
h1 {
    text-align: center;
}

</style>