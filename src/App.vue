<template>
  <div id="app" class="container">
    <div class="jumbotron">
      <div class="shopping-header">
        <h2>{{ title.toUpperCase() }}</h2>

        <button
          v-if="!isInputShown"
          type="button"
          class="btn btn-primary"
          @click="toggleInput(true)"
        >Add Item</button>
        
        <button v-else type="button" class="btn btn-danger" @click="toggleInput(false)">Cancel</button>
      </div>

      <div v-if="isInputShown" class="shopping-form">
        <input
          v-model="newItem"
          type="text"
          class="form-control"
          placeholder="Add an item"
          @keyup.enter="saveItems"
        >
        
        <span>{{ charCount }}/200</span>
        
        <button type="button" class="btn btn-primary" @click="saveItems">Save Item</button>
      </div>

      <ul>
        <li
          v-for="(item, index) in reversedItems"
          class="item-list"
          :class="{'purchased' : item.purchased }"
          :key="index"
          @click="togglePurchased(item)"
        >{{ item.label }}</li>
      </ul>

      <p v-if="items.length === 0">No item should be bought!</p>

      <a :href="urlLink" target="_blank">Mamikos</a>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",

  data() {
    return {
      title: "shopping list",
      items: [
        {
          label: "1kg telur",
          purchased: false
        },
        {
          label: "2kg tepung terigu",
          purchased: false
        },
        {
          label: "1/2kg gula pasir",
          purchased: true
        }
      ],
      newItem: "",
      isInputShown: false,
      urlLink: "https://mamikos.com"
    };
  },

  computed: {
    charCount() {
      return this.newItem.length;
    },
    reversedItems() {
      return this.items.slice(0).reverse();
    }
  },

  methods: {
    saveItems() {
      this.items.push({
        label: this.newItem,
        purchased: false
      });
      this.newItem = "";
    },
    toggleInput(state) {
      this.isInputShown = state;
    },
    togglePurchased(item) {
      item.purchased = !item.purchased;
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

.jumbotron {
  box-shadow: 5px 5px 10px grey;
}

.jumbotron h2 {
  font-weight: bold;
  margin-bottom: 15px;
}

.jumbotron ul {
  margin-top: 15px;
}

.jumbotron li {
  margin: 5px 0;
  cursor: pointer;
}

.shopping-header {
  margin-bottom: 20px;
}

.shopping-form input {
  float: left;
  width: 70%;
  margin-right: 5px;
}

.shopping-form button {
  margin-left: 20px;
}

.item-list {
  color: orange;
}

.purchased {
  text-decoration: line-through;
  color: lightgrey;
}
</style>
