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
          name: 'Granactive Retinoid 2% in Squalane',
          type: 'retinoid',
          type_id: 1,
        },
        {
          id: 2,
          name: 'Granactive Retinoid 5% in Squalane',
          type: 'retinoid',
          type_id: 1,
        },
        {
          id: 3,
          name: 'Granactive Retinoid 2% Emulsion ',
          type: 'retinoid',
          type_id: 1,
        },
        {
          id: 4,
          name: 'Advanced Retinoid 2%',
          type: 'retinoid',
          type_id: 1,
        },
        {
          id: 5,
          name: 'Retinol 0.2% in Squalane',
          type: 'retinoid',
          type_id: 1,
        },
        {
          id: 6,
          name: 'Retinol 0.5% in Squalane',
          type: 'retinoid',
          type_id: 1,
        },
        {
          id: 7,
          name: 'Retinol 1% in Squalane',
          type: 'retinoid',
          type_id: 1,
        },
        {
          id: 8,
          name: 'Ascorbyl Glucoside Solution 12%',
          type: 'water-based',
          type_id: 2,
        },
        {
          id: 9,
          name: '"B" Oil',
          type: 'hydrator',
          type_id: 3
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

      // beginning of sort functions
      this.oneTypeOnly(this.selectedItems, 'type_id', 1); // only 1 retinol can exist in list

      this.beforeSameAttrDifferentVal(this.selectedItems, 'type_id', 1, 2); // retinol must come before water
      this.beforeSameAttrDifferentVal(this.selectedItems, 'type_id', 1, 3); // retinol must come before oil
      this.beforeSameAttrDifferentVal(this.selectedItems, 'type_id', 2, 3); // water based must come before oil
    },
    removeFromSelected(id) {
      let allSelectedItems = this.selectedItems;

      let itemIndex = allSelectedItems.findIndex(item => item.id === id);

      this.selectedItems.splice(itemIndex, 1);

      // beginning of sort functions, must be checked on delete as well
      this.oneTypeOnly(this.selectedItems, 'type_id', 1);
    },
    oneTypeOnly(array, attr, value) {
      let counter = 0;
      for(var i = 0; i < array.length; i += 1) {
          if(array[i][attr] === value) {
            counter +=1
            if(counter > 1) {
              console.log("too many " + attr + value );
            } else {
              console.log("one " + attr + value + " perfect!" );
            }
          }
      }
    },
    beforeSameAttrDifferentVal(array, attr, value_1, value_2) {

      let swapped;
      do {
        swapped = false;
        for (let i = 0; i < array.length; i += 1) {
          if(typeof array[i + 1] !== 'undefined') {

            if (array[i][attr] === value_2 && array[i + 1][attr] === value_1) {
              let tmp = array[i];
              array[i] = array[i + 1];
              array[i + 1] = tmp;
              swapped = true;
            }

          }
        }
      } while (swapped);
      // for(var i = 0; i < array.length; i += 1) {
      //     // if( swap ) {
      //       if(array[i][attr] === value_2 && array[i + 1][attr] === value_1) {
      //         let b = array[i];
      //         array[i] = array[i + 1];
      //         array[i + 1] = b;
      //       }
      //       // else {
      //       //   swap = false;
      //       // }
      //     // }
      // }
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
