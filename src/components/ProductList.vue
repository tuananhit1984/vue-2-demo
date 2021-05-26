<template>
  <div class="layout">
    <h1>{{ productName }}</h1>
    
    <span>Search: </span> <input type="text" v-model="productSearchQuery" placeholder="product name" />
    <h3>Tổng số lượng: {{ total }}</h3>
    <ul>
        <li v-for="product in productDataListFiltered" :key="product.id">
            {{ product.name }}
        </li>
    </ul>
  </div>
</template>

<script>
import { productData } from './../type/Product';

export default {
  name: 'ProductList',
  props: {
    productName: String
  },
  data() {
      return {
          productDataListFiltered: {},
          productSearchQuery: ''
      }
  },
  computed: {
      total: function() {
        return this.productDataListFiltered.length;
      },
  },
  watch: {
    productSearchQuery: function (searchQuery) {
       this.filterProductByName(searchQuery);
    },
  },
  methods: {
    filterProductByName(searchQuery) {
        if (searchQuery) {
            this.productDataListFiltered = productData.filter(p => p.name.toLowerCase().includes(searchQuery));
        } else {
            this.productDataListFiltered = productData;
        }
    }
  },
  mounted() {
      this.filterProductByName();
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.layout {
    width: 250px;
    margin: 0 auto;
}
ul {
  list-style-type: none;
  padding: 0;
  text-align: left;
}
li {
  margin: 0 10px;
  padding: 5px 0;
  border-bottom: 1px solid;
}
ul li:last-child {
    border-bottom: none;
}
h3 {
    text-align: left;
    padding-left: 5px;
}
</style>
