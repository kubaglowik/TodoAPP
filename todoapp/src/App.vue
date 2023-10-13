<template>
  <div class="all">
    <div class="item">
      <atom-input type="text" class="text" placeholder="add task" v-model="newitem" @keyup.enter="addItem"/>
      <atom-button text="ADD" class="additem" @click="showDataandadditem"></atom-button>
      <atom-select name="sort" class="sort" @change="sortList">
        <atom-option text="a-z" value="az" />
        <atom-option text="z-a" value="za" />
        <atom-option text="old to new" value="stn" />
        <atom-option text="new to old" value="nts" />
      </atom-select>
    </div>
    <div :class="{'item2': true, 'status': item.status}" v-for="item in items" :key="item.id">
      <div class="data">
      <p>{{ item.data2 }}</p>
      </div>
      <atom-header :text="item.title" />
      <atom-button text="Ready" class="additem" v-if="!item.status" @click="removeitem(item.id)"></atom-button>
      <atom-button text="Delete" class="delete" v-if="item.avilable === 0" @click="deleteeitem(item.id)"></atom-button>
    </div>
  </div>
</template>

<script>
import AtomOption from './components/Atoms/AtomOption.vue';
import AtomButton from './components/Atoms/AtomButton.vue';
import AtomHeader from './components/Atoms/AtomHeader.vue';
import AtomInput from "./components/Atoms/AtomInput.vue";
import AtomSelect from './components/Atoms/AtomSelect.vue';


export default {
  components: {
    AtomInput, AtomButton, AtomHeader, AtomSelect, AtomOption
  },

  data() {
    return {
      newitem: "",
      items: [],
      isDataAvailable: false, // Dodaj tę zmienną
    };
  },
  methods: {

    addItem() {
      this.items.push({
        title: this.newitem, status: false, id: Math.random(), avilable: 0, data:new Date(),data2: new Date().toLocaleString(),
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
    sortList(event) {
      const msec = Date.parse(new Date);
      console.log(msec)
      const selectValue = event.target.value;
      if (selectValue === 'za') {
        this.items = this.items.sort((item1, item2) => {
          if (item1.title > item2.title) {
            return -1;
          }

          return 1;
        })
      }
      if (selectValue === 'az') {
        this.items = this.items.sort((item1, item2) => {
          if (item1.title < item2.title) {
            return -1;
          }

          return 1;
        })
      }
      if (selectValue === 'stn') {
        this.items = this.items.sort((item1, item2) => {
          if (item1.data < item2.data) {
            return -1;
          }

          return 1;
        })
      }
      if (selectValue === 'nts') {
        this.items = this.items.sort((item1, item2) => {
          if (item1.data > item2.data) {
            return -1;
          }

          return 1;
        })
      }
    },

    showData() {

    },
    showDataandadditem() {
      this.showData();
      this.addItem();
    },

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
.all {
  min-height: 100vh;
  min-width: 100%;
  background-size: cover;
  background-attachment: fixed;
  display: flex;
  align-items: center;
  flex-direction: column;
  font-family: "Montserrat", sans-serif !important;
  font-weight: 500;
  background-color: red;
  background: rgb(0, 213, 255);
  background: linear-gradient(176deg, rgba(0, 213, 255, 1) 0%, rgba(0, 127, 255, 1) 100%);
}

.item {

  margin-top: 5%;
  padding: 10px;
  width: 80%;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgb(255, 255, 255);
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  border-radius: 10px;
}

.item2 {
  margin: 10px;
  padding: 10px;
  min-width: 70%;
  width: fit-content;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  font-family: "Montserrat", sans-serif !important;
  font-weight: 1000;
  background-color: rgb(255, 255, 255);
  border-radius: 15px;
}

.text {
  width: 50%;
  padding: 5px 5px;
  border: none;
  border-radius: 4px;
  background-color: #f1f1f1;
}

.sort {
  width: 20%;
  padding: 5px 5px;
  border: none;
  border-radius: 10px;
  background-color: #f1f1f1;
}

.additem {
  width: 10%;
  padding: 5px 5px;
  border: none;
  border-radius: 4px;
  background-color: #f1f1f1;
}

.status {
  opacity: 70%;
}

.status h2 {
  text-decoration: line-through;
  color: rgb(255, 0, 0);
}

.additem {
  margin: 10px;
}

.delete {
  color: red;
  width: 10%;
  padding: 5px 5px;
  border: none;
  border-radius: 4px;
  background-color: #f1f1f1;

}

* {
  scrollbar-width: none;
  scrollbar-color: #00aaff #ffffff;
}

*::-webkit-scrollbar {
  width: 6px;
}

*::-webkit-scrollbar-track {
  background: #ffffff;
}

*::-webkit-scrollbar-thumb {
  background-color: #00aaff;
  border-radius: 9px;
  border: 0px solid #ffffff;
}

@media screen and (min-width: 425px) {
  .item {
    width: 80%;
  }

  .item2 {
    min-width: 70%;
  }

  .additem {
    width: 15%;
  }

  .delete {
    width: 15%;
  }
}

@media screen and (min-width: 375px) {
  .item {
    width: 80%;
  }

  .item2 {
    min-width: 70%;
  }

  .additem {
    width: 15%;
  }

  .delete {
    width: 15%;
  }
}

@media screen and (min-width: 320px) {
  .item {
    width: 80%;
  }

  .item2 {
    min-width: 70%;
  }

  .additem {
    width: 15%;
  }

  .delete {
    width: 15%;
  }
}</style>
