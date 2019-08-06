<template lang="html">
  <section class="row">
    <div class="column">
      <h1>Product List</h1>

      <input type="text" v-model="search">

      <ul>
          <li v-for="item in filteredItems"
          @click="addToSelected(item.id)"
          v-bind:key="item.id"
          >
          {{ item.name }} id: {{item.type_id}}
        </li>
      </ul>
    </div>

    <div class="column">
      <h1>To Dew</h1>

      <ul>
        <li v-for="item in selectedItems"
        v-bind:key="item.id">
          {{ item.name }} id: {{item.type_id}}
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
          name: 'Ascorbic Acid 8% + Alpha Arbutin 2%',
          type: 'vitamin-c',
          type_id: 4
        },
        {
          id: 9,
          name: 'Ascorbyl Glucoside Solution 12%',
          type: 'vitamin-c',
          type_id: 4
        },
        {
          id: 10,
          name: 'Ascorbyl Tetraisopalmitate Solution 20% in Vitamin F',
          type: 'vitamin-c',
          type_id: 4
        },
        {
          id: 11,
          name: 'Ethylated Ascorbic Acid 15% Solution',
          type: 'vitamin-c',
          type_id: 4
        },
        {
          id: 12,
          name: 'Magnesium Ascorbyl Phosphate 10%',
          type: 'vitamin-c',
          type_id: 4
        },
        {
          id: 13,
          name: 'Vitamin C Suspension 23% + HA Spheres 2%',
          type: 'vitamin-c',
          type_id: 4
        },
        {
          id: 14,
          name: 'Vitamin C Suspension 30% in Silicone',
          type: 'vitamin-c',
          type_id: 4
        },
        {
          id: 15,
          name: 'AHA 30% + BHA 2% Peeling Solution',
          type: 'water-based, direct-acid',
          type_id: 2
        },
        {
          id: 16,
          name: 'Alpha Lipoic Acid 5%',
          type: 'water-based',
          type_id: 2
        },
        {
          id: 17,
          name: 'Azelaic Acid Suspension 10%',
          type: 'water-based, direct-acid',
          type_id: 2
        },
        {
          id: 18,
          name: 'Glycolic Acid 7% Toning Solution',
          type: 'water-based, direct acid',
          type_id: 2
        },
        {
          id: 19,
          name: 'Lactic Acid 5% + HA',
          type: 'water-based, direct-acid',
          type_id: 2
        },
        {
          id: 20,
          name: 'Lactic Acid 10% + HA',
          type: 'water-based, direct-acid',
          type_id: 2
        },
        {
          id: 21,
          name: 'Mandelic Acid 10% + HA',
          type: 'water-based, direct-acid',
          type_id: 2
        },
        {
          id: 22,
          name: 'Salicylic Acid 2% Solution',
          type: 'water-based, direct-acid',
          type_id: 2
        },
        {
          id: 23,
          name: 'Alpha Lipoic Acid 5%',
          type: 'antioxidants',
          type_id: 6
        },
        {
          id: 24,
          name: 'EUK 134 0.1%',
          type: 'antioxidants',
          type_id: 6
        },
        {
          id: 25,
          name: 'Resveratrol 3% + Ferulic Acid 3%',
          type: 'antioxidants',
          type_id: 6
        },
        {
          id: 26,
          name: 'Pycnogenol 5%',
          type: 'antioxidants',
          type_id: 6
        },
        {
          id: 27,
          name: '"B" Oil',
          type: 'oil',
          type_id: 3
        },
        {
          id: 28,
          name: '100% Organic Cold-Pressed Borage Seed Oil',
          type: 'oil',
          type_id: 3
        },
        {
          id: 29,
          name: '100% Organic Cold-Pressed Moroccan Argan Oil',
          type: 'oil',
          type_id: 3
        },
        {
          id: 30,
          name: '100% Organic Cold-Pressed Rose Hip Seed Oil',
          type: 'oil',
          type_id: 3
        },
        {
          id: 31,
          name: '100% Organic Virgin Chia Seed Oil',
          type: 'oil',
          type_id: 3
        },
        {
          id: 32,
          name: '100% Cold-Pressed Virgin Marula Oil',
          type: 'oil',
          type_id: 3
        },
        {
          id: 33,
          name: '100% Organic Virgin Sea-Buckthorn Fruit Oil',
          type: 'oil',
          type_id: 3
        },
        {
          id: 34,
          name: '100% Plant-Derived Squalane',
          type: 'oil',
          type_id: 3
        },
        {
          id: 35,
          name: '100% Plant-Derived Squalane',
          type: 'oil',
          type_id: 3
        },
        {
          id: 36,
          name: 'Amino Acids + B5',
          type: 'water',
          type_id: 2
        },
        {
          id: 37,
          name: 'Hyaluronic Acid 2% + B5',
          type: 'water',
          type_id: 2
        },
        {
          id: 38,
          name: 'Marine Hyaluronics',
          type: 'water',
          type_id: 2
        },
        {
          id: 39,
          name: 'Natural Moisturizing Factors + HA',
          type: 'oil, last',
          type_id: 3
        },
        {
          id: 40,
          name: '100% Plant-Derived Hemi-Squalane',
          type: 'oil',
          type_id: 3
        },
        {
          id: 41,
          name: 'Alpha Arbutin 2% + HA',
          type: 'water, more molecules',
          type_id: 2
        },
        {
          id: 42,
          name: 'Argireline Solution 10%',
          type: 'water, more molecules',
          type_id: 2
        },
        {
          id: 43,
          name: '"Buffet"',
          type: 'peptide',
          type_id: 7
        },
        {
          id: 44,
          name: '“Buffet” + Copper Peptides 1%',
          type: 'peptide',
          type_id: 7
        },
        {
          id: 45,
          name: 'Caffeine Solution 5% + EGCG',
          type: 'peptide',
          type_id: 7
        },
        {
          id: 46,
          name: 'Matrixyl 10% + HA',
          type: 'peptide',
          type_id: 7
        },
        {
          id: 47,
          name: 'Niacinamide 10% + Zinc 1%',
          type: 'peptide',
          type_id: 7
        },
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
      this.tooManyProducts(this.selectedItems);

      this.oneTypeOnly(this.selectedItems, 'type_id', 1);

      this.conflictTypeID(this.selectedItems, 'type_id', 7, [6,4]);

      // retinol before water-based, oil, vitamin c, antioxidants, peptides
      this.beforeSameAttrDifferentVal(this.selectedItems, 'type_id', 1, [2,3,4,6,7]);
      do {
          this.beforeSameAttrDifferentVal(this.selectedItems, 'type_id', 2, [3,4,6,7]);
          this.beforeSameAttrDifferentVal(this.selectedItems, 'type_id', 6, [3]);
          this.beforeSameAttrDifferentVal(this.selectedItems, 'type_id', 7, [3]);
      } while (this.beforeSameAttrDifferentVal(this.selectedItems, 'type_id', 1, [2,3,4,6,7]));

      // water-based before oil
      this.beforeSameAttrDifferentVal(this.selectedItems, 'type_id', 2, [3,4,6,7]);
      do {
        this.beforeSameAttrDifferentVal(this.selectedItems, 'type_id', 1, [2,3,4,6,7]);
        this.beforeSameAttrDifferentVal(this.selectedItems, 'type_id', 6, [3]);
        this.beforeSameAttrDifferentVal(this.selectedItems, 'type_id', 7, [3]);
      } while (this.beforeSameAttrDifferentVal(this.selectedItems, 'type_id', 2, [3,4,6,7]));

      // antioxidants before oil
      this.beforeSameAttrDifferentVal(this.selectedItems, 'type_id', 6, [3]);
      do {
        this.beforeSameAttrDifferentVal(this.selectedItems, 'type_id', 1, [2,3,4,6,7]);
        this.beforeSameAttrDifferentVal(this.selectedItems, 'type_id', 2, [3,4,6,7]);
        this.beforeSameAttrDifferentVal(this.selectedItems, 'type_id', 7, [3]);
      } while (this.beforeSameAttrDifferentVal(this.selectedItems, 'type_id', 6, [3]));

      // peptides before oil
      this.beforeSameAttrDifferentVal(this.selectedItems, 'type_id', 7, [3]);
      do {
        this.beforeSameAttrDifferentVal(this.selectedItems, 'type_id', 1, [2,3,4,6,7]);
        this.beforeSameAttrDifferentVal(this.selectedItems, 'type_id', 2, [3,4,6,7]);
        this.beforeSameAttrDifferentVal(this.selectedItems, 'type_id', 6, [3]);
      } while (this.beforeSameAttrDifferentVal(this.selectedItems, 'type_id', 7, [3]));

    },
    removeFromSelected(id) {
      let allSelectedItems = this.selectedItems;

      let itemIndex = allSelectedItems.findIndex(item => item.id === id);

      this.selectedItems.splice(itemIndex, 1);

      // beginning of sort functions, must be checked on delete as well
      this.oneTypeOnly(this.selectedItems, 'type_id', 1);

      this.tooManyProducts(this.selectedItems);

      this.conflictTypeID(this.selectedItems, 'type_id', 7, [6,4]);
    },
    tooManyProducts(array) {
      if(array.length === 5) {
        console.log("You sure you need 5 products?");
      } else if (array.length === 6) {
        console.log("Six is a lot of things, make sure you know what you're doing.");
      } else if (array.length >= 7) {
        console.log( array.length + "is a lot! You still need room for a face mask dude.");
      }
    },
    oneTypeOnly(array, attr, value) {
      let counter = 0;
      for(var i = 0; i < array.length; i += 1) {
          if(array[i][attr] === value) {
            counter +=1
            if(counter > 1) {
              // console.log("too many " + attr + value );
            } else {
              // console.log("one " + attr + value + " perfect!" );
            }
          }
      }
    },
    conflictTypeID(array, attr, value_1, value_2) {
      let counter = 0;
      for(var i = 0; i < array.length; i +=1) {
        if(typeof array[i + 1] !== 'undefined') {

            if (array[i][attr] === value_1 || (value_2.indexOf(array[i][attr]) !== -1) ) {
              counter +=1;
              
              if(counter > 0) {
                console.log("you cant have " + attr + value_1 + ' and ' + value_2 + ' together' );
              } else if(counter === 0)  {
                console.log("no conflicts");
              }
            }


        }
      }
    },
    beforeSameAttrDifferentVal(array, attr, value_1, value_2) {
      let swapped;
      do {
        swapped = false;
        for(var i = 0; i < array.length; i += 1) {
          if(typeof array[i + 1] !== 'undefined') {

            if( (value_2.indexOf(array[i][attr]) !== -1) && array[i + 1][attr] === value_1) {
              let b = array[i];
              array[i] = array[i + 1];
              array[i + 1] = b;
              swapped = true;
            }
          }
        }
      } while (swapped);
      return swapped;
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
