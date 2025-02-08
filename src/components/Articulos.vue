<template>
    <div class="container py-4">
      <div class="row g-4">
        <div 
          v-for="articulo in articulos" 
          :key="articulo.id" 
          class="col-12 col-md-6 col-lg-4"
        >
          <div class="card h-100 shadow-sm">
            <img 
              :src="articulo.imagen" 
              :alt="articulo.nombre" 
              class="card-img-top"
            />
            <div class="card-body">
              <h5 class="card-title fw-bold">{{ articulo.nombre }}</h5>
              <p class="card-text">{{ articulo.descripcion }}</p>
              <p class="mb-1"><strong>Marca:</strong> {{ articulo.marca }}</p>
              <p class="mb-3"><strong>Precio:</strong> ${{ articulo.precio.toFixed(2) }}</p>
              <button
                @click="agregarAlCarrito(articulo)"
                class="btn btn-success w-100"
              >
                Añadir al carrito
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import { articulos } from "../data/Articulos";
  
  export default {
    name: "Articulos",
    data() {
      return {
        articulos,
      };
    },
    methods: {
      agregarAlCarrito(articulo) {
        this.$emit("add-to-cart", articulo);
      },
    },
  };
  </script>
  
  <style scoped>
  .card-img-top {
    height: 200px;
    object-fit: cover;
  }
  </style>
  