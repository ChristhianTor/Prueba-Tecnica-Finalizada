 
<template>
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>Nombre</th>
          <th>Precio</th>
          <th>Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="product in products" :key="product.id">
          <td>{{ product.id }}</td>
          <td>{{ product.name }}</td>
          <td>{{ product.price }}</td>
          <td>
            <button @click="$emit('edit-product', product)">Editar</button>
            <button @click="deleteProduct(product.id)">Eliminar</button>
          </td>
        </tr>
      </tbody>
    </table>
  </template>
  
  <script>
  export default {
    props: ['products'],
    methods: {
      async deleteProduct(id) {
        await fetch(`http://127.0.0.1:5000/products/${id}`, { method: 'DELETE' });
        this.$emit('product-saved');  // Emitir evento al componente padre
      }
    }
  };
  </script>
  