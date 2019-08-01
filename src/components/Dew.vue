<template lang="html">
  <section class="row">
    <div class="column">
      <h1>Product List</h1>

      <input type="text" v-model="search">

      <ul>
          <li v-for="(item, index) in filteredItems"
          @click="addToSelected(item.id)"
          :key="item.id"
          >
          {{ item.name }}
        </li>
      </ul>
    </div>

    <div class="column">
      <h1>To Dew</h1>

      <ul>
        <li v-for="item in selectedItems">
          {{ item.name }}
          <span
          @click="removeFromSelected(item.id)">X</span>
        </li>
      </ul>

    </div>
<!--
    <button>Sort</button> -->

  </section>
</template>

<script>
export default {
  props: {
    id: Number,
    name: String
  },
  data() {
    return {
      active: false,
      search: '',
      selectedItems: [],
      items: [
        {
          id: 1,
          name: 'Advanced Retinoid 2%',
          type: 'retinoid'
        },
        {
          id: 2,
          name: 'Ascorbyl Glucoside Solution 12%',
          type: 'water-based'
        },
        {
          id: 3,
          name: '"B" Oil',
          type: 'hydrator'
        }
      ]
    }
  },
  methods: {
    addToSelected(id) {
      let allItems = this.items;
      let item = allItems.find(e => e.id === id);

      // if item doesn't exist add to array
      let found = this.selectedItems.some(e => e.id === id);
      if (!found) {
        this.selectedItems.push(item);
      }
    },
    removeFromSelected(id) {
      let allItems = this.items;
      let item = allItems.find(e => e.id === id);
      this.selectedItems.pop(item);
    },
    sortSelected() {

    }
  },
  computed: {
    filteredItems() {
      return this.items.filter(item => {
         return item.name.toLowerCase().indexOf(this.search.toLowerCase()) > -1
      })
    },
  }
}
</script>

<style lang="css" scoped>

input, button {
  border: 2px solid #000;
  margin-bottom: 1em;
  margin-top: 1em;
}

.hover {
  background: rgb(244, 244, 244);
  border-radius: 10px;
}

li {
  cursor: pointer;
}

.row {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  width: 100%;
}

.column {
  display: flex;
  flex-direction: column;
  flex-basis: 100%;
  flex: 1;
}

</style>
