<template>
  <div>
    <h2>{{ isEditing ? 'Editar Producto' : 'Agregar Producto' }}</h2>
    <form @submit.prevent="saveProduct">
      <input v-model="product.name" placeholder="Nombre" required />
      <input v-model.number="product.price" type="number" placeholder="Precio" required />
      <button type="submit">{{ isEditing ? 'Actualizar' : 'Guardar' }}</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      product: { name: '', price: 0 },
      isEditing: false,
      productId: null
    };
  },
  methods: {
    async saveProduct() {
      const url = this.isEditing
        ? `http://127.0.0.1:5000/products/${this.productId}`
        : 'http://127.0.0.1:5000/products';

      const method = this.isEditing ? 'PUT' : 'POST';

      await fetch(url, {
        method,
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(this.product)
      });

      this.$emit('product-saved');  // Emitir evento al componente padre
      this.resetForm();
    },
    setProduct(product) {
      this.product = { ...product };
      this.productId = product.id;
      this.isEditing = true;
    },
    resetForm() {
      this.product = { name: '', price: 0 };
      this.isEditing = false;
      this.productId = null;
    }
  }
};
</script>
