<template>
  <div id="app">
    <div class="container">
      <h1>Gestión de Productos</h1>
      <ProductForm @product-saved="fetchProducts" ref="productForm" />
      <ProductList :products="products" @edit-product="editProduct" />
    </div>
  </div>
</template>

<script>
import ProductForm from './components/ProductForm.vue';
import ProductList from './components/ProductList.vue';

export default {
  components: {
    ProductForm,
    ProductList
  },
  data() {
    return {
      products: []  // Estado para almacenar los productos
    };
  },
  methods: {
    async fetchProducts() {
      const response = await fetch('http://127.0.0.1:5000/products');
      this.products = await response.json();
    },
    editProduct(product) {
      this.$refs.productForm.setProduct(product);  // Configura el producto a editar
    }
  },
  mounted() {
    this.fetchProducts();  // Cargar los productos al montar el componente
  }
};
</script>

<style scoped>
.container {
  margin-top: 20px;
}
</style>
