<template>
<div class="all">
  <div class="item">
    <!-- <p>{{showData}}</p> -->
    <atom-input type="text" placeholder="add task" v-model="newitem" @keyup.enter="addItem"></atom-input>
    <atom-button :text="'ADD'" class="additem" @click="addItem"></atom-button>
    <atom-select name="sort" id="sort" @change="sortList">
      <atom-option :text="'a-z'" value="az"/>
      <atom-option :text="'z-a'" value="za"/>
      <atom-option :text="'old to new'" value="stn"/>
      <atom-option :text="'new to old'" value="nts"/>
    </atom-select>
  </div>
  <div class="item" v-bind:class="{ status: item.status }" v-for="item in items" v-bind:key="item.id">
    <atom-header :text="item.title"/>
    <atom-button :text="'Ready'" class="additem" v-if="!item.status" @click="removeitem(item.id)"></atom-button>
    <atom-button :text="'Delete'" class="delete" v-if="item.avilable === 0" @click="deleteeitem(item.id)"></atom-button>
  </div>
  </div>
</template>

<script>
import AtomOption from './components/AtomOption.vue';
import AtomButton from './components/Atoms/AtomButton.vue';
import AtomHeader from './components/Atoms/AtomHeader.vue';
import AtomInput from "./components/Atoms/AtomInput.vue";
import AtomSelect from './components/Atoms/AtomSelect.vue';


export default {
  components: {
    AtomInput, AtomButton,AtomHeader,AtomSelect,AtomOption
  },

  data() {
    return {
      newitem: "",
      items: [],
    };
  },
  methods: {
    
    addItem() {
      this.items.push({ title: this.newitem, status: false, id: Math.random(), avilable: 0, data: new Date,
      });
       localStorage.setItem('items', JSON.stringify(this.items));
        this.newitem = ""; 
    },
    removeitem(id) {
      const index = this.items.findIndex((el) => el.id === id);
      this.items[index].status = true;
      localStorage.setItem('items', JSON.stringify(this.items));
    },
    deleteeitem(id) {
      const index = this.items.findIndex((el) => el.id === id);
      this.items.splice(index, 1).avilable = 1;
      localStorage.setItem('items', JSON.stringify(this.items));
    },
    sortList(event){
          const msec = Date.parse(new Date);
      console.log(msec)
      const selectValue = event.target.value;
      if(selectValue === 'za'){
        this.items = this.items.sort((item1, item2) => {
          if(item1.title > item2.title) {
            return -1;
          }

          return 1;
        })
      }
      if(selectValue === 'az'){
        this.items = this.items.sort((item1, item2) => {
          if(item1.title < item2.title) {
            return -1;
          }

          return 1;
        })
      }
      if(selectValue === 'stn'){
        this.items = this.items.sort((item1, item2) => {
          if(item1.data < item2.data) {
            return -1;
          }

          return 1;
        })
      }
      if(selectValue === 'nts'){
        this.items = this.items.sort((item1, item2) => {
          if(item1.data > item2.data) {
            return -1;
          }

          return 1;
        })
      }
    },

    // showData() {
    //   const msec = Date.parse(new Date);
    //   console.log(msec)
    //   const itemdata = (new Date)
    //   console.log(itemdata);
    // },

  },
  mounted() {
    const storedItems = localStorage.getItem('items');
    if (storedItems) {
      this.items = JSON.parse(storedItems);
    }
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
