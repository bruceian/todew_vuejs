<template lang="html">
  <section class="row">
    <div class="products column">
        <h1>Product List</h1>
        <div class="form-group">
          <input
            type="text"
            v-model="input"
            placeholder="Enter product"
            class="form-control"
          />
        </div>

        <ul v-for="(product, index) in filteredProductSearch" class="list-group">
          <li class="list-group-item"
            :key="product.name"
            >
            {{ product.name }}
          </li>
        </ul>
    </div>

    <div class="to-dew column">
        <h1>To Dew</h1>

    </div>
  </section>
</template>

<script>
export default {
  name: 'List',
  props: {
    name: String,
    type: String
  },
  data() {
    return {
      input: '',
      products: [
        {
          name: 'Advanced Retinoid 2%',
          type: 'retinoid'
        },
        {
          name: 'Ascorbyl Glucoside Solution 12%',
          type: 'water-based'
        },
        {
          name: '"B" Oil',
          type: 'hydrator'
        },
      ],
      selected: [],

    }
  },
  // methods: {
  //   addToSelectedArray() {
  //
  //   }
  // },
  computed: {
    filteredProductSearch() {
      return this.products.filter(product =>
        product.name.toLowerCase().includes(this.input.toLowerCase())
      );
    }
  }
}
</script>

<style lang="css" scoped>
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
