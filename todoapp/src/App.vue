<template>
  <div class="item">
    <input type="text" placeholder="add task" v-model="newitem">
    <button class="additem" @click="addItem">add</button>
  </div>
  <div class="item" v-bind:class="{ status: item.status }" v-for="item in items" v-bind:key="item.id">
    <h2>{{ item.title }}</h2>
    <button class="additem" v-if="!item.status" @click="removeitem(item.id)">ready</button>
    <button class="delete" v-if="item.avilable==0" @click="deleteeitem(item.id)">delete</button>
  </div>
  <div id="app">
    <MyComponent />
  </div>
</template>

<script>
import MyComponent from './components/MyComponent.vue'

export default {
  data() {
    return {
      newitem: "default",
      items: [
      ]
    }
  },
  methods: {
    addItem() {
      this.items.push({ title: this.newitem, status: false, id: Math.random(), avilable:0})
    },
    removeitem(id) {
      const index = this.items.findIndex(el => el.id === id)
      this.items[index].status = true
    },
    deleteeitem(id) {
      const index = this.items.findIndex(el => el.id === id)
      this.items.splice(index,1).avilable = 1
    },
  },
  name: 'App',
  components: {
    MyComponent
  }
}
</script>
<style>
template {
  display: flex;  
  justify-content: center;

}

.main {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}

.item {
  border: 1px solid #333;
  margin-top: 5px;
  padding: 10px;
  width: 500px;
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}

.status {
  opacity: 50%;
}

.status h2 {
  text-decoration: line-through;
  color: rgb(0, 140, 255);
}

.additem {
  margin: 10px;
}
.delete{
color: red;
}
.avilable
{
  background-color:red;
}
</style>
