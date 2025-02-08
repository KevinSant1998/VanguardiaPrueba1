<template>
    <div class="container py-4">
      <h2 class="text-center fw-bold mb-4">🛒 Carrito de Compras</h2>
      <div v-if="carrito.length === 0" class="alert alert-info text-center">
        El carrito está vacío.
      </div>
      <div v-else>
        <div
          v-for="(item, index) in carrito"
          :key="index"
          class="d-flex align-items-center justify-content-between border-bottom py-3"
        >
          <img 
            :src="item.imagen" 
            :alt="item.nombre" 
            class="rounded" 
            style="width: 70px; height: 70px; object-fit: cover;" 
          />
  
          <div class="flex-grow-1 px-3">
            <h5 class="mb-1">{{ item.nombre }}</h5>
            <p class="mb-0 text-muted">${{ item.precio.toFixed(2) }}</p>
          </div>
  
          <div class="d-flex align-items-center">
            <button 
              @click="decrementarCantidad(index)" 
              class="btn btn-outline-secondary btn-sm me-2"
            >
              ➖
            </button>
            <span class="fw-bold">{{ item.cantidad }}</span>
            <button 
              @click="incrementarCantidad(index)" 
              class="btn btn-outline-secondary btn-sm ms-2"
            >
              ➕
            </button>
          </div>
        </div>
  
        <div class="text-end mt-4">
          <h4><strong>Total:</strong> ${{ total.toFixed(2) }}</h4>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: "Cart",
    props: ["carrito"],
    computed: {
      total() {
        return this.carrito.reduce((sum, item) => sum + item.precio * item.cantidad, 0);
      },
    },
    methods: {
      incrementarCantidad(index) {
        this.$emit("update-quantity", index, 1);
      },
      decrementarCantidad(index) {
        this.$emit("update-quantity", index, -1);
      },
    },
  };
  </script>
  
  <style scoped>
  </style>
  