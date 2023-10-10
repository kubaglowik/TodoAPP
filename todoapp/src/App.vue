<template>
  <div class="item">
    <atom-input type="text" placeholder="add task" v-model="newitem"></atom-input>
    <button class="additem" @click="addItem">add</button>
    <select name="sort" id="sort" @change="change">
      <option value="az">a-z</option>
      <option value="za">z-a</option>
      <option value="stn">old to new</option>
      <option value="nts">new to old</option>
    </select>
  </div>
  <div
    class="item"
    v-bind:class="{ status: item.status }"
    v-for="item in items"
    v-bind:key="item.id">
    <h2>{{ item.title }}</h2>
    <atom-button v-text="'Ready'" class="additem" v-if="!item.status" @click="removeitem(item.id)"></atom-button>
    <atom-button v-text="'Delete'" class="delete" v-if="item.avilable == 0" @click="deleteeitem(item.id)"></atom-button>
  </div>
</template>

<script>
import AtomButton from './components/Atoms/AtomButton.vue';
import AtomInput from "./components/Atoms/AtomInput.vue";


export default {
  components: {
    AtomInput, AtomButton
  },

  data() {
    return {
      newitem: "",
      items: [],
    };
  },
  methods: {
    addItem() {
      this.items.push({
        title: this.newitem,
        status: false,
        id: Math.random(),
        avilable: 0,
      });
    },
    removeitem(id) {
      const index = this.items.findIndex((el) => el.id === id);
      this.items[index].status = true;
    },
    deleteeitem(id) {
      const index = this.items.findIndex((el) => el.id === id);
      this.items.splice(index, 1).avilable = 1;
    },
    // change(){
    //   if(items==0)
    // },
  },
};
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
.delete {
  color: red;
}
.avilable {
  background-color: red;
}
</style>
