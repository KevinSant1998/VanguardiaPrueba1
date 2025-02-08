<script>
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";
import Articulos from "./components/Articulos.vue";
import Cart from "./components/Cart.vue";

export default {
  name: "App",
  components: { Header, Footer, Articulos, Cart },
  data() {
    return {
      carrito: JSON.parse(localStorage.getItem("carrito")) || [],
    };
  },
  methods: {
    agregarAlCarrito(articulo) {
      const item = this.carrito.find((i) => i.id === articulo.id);
      if (item) {
        item.cantidad++;
      } else {
        this.carrito.push({ ...articulo, cantidad: 1 });
      }
      this.guardarCarrito();
    },
    actualizarCantidad(index, cantidad) {
      this.carrito[index].cantidad += cantidad;
      if (this.carrito[index].cantidad <= 0) {
        this.carrito.splice(index, 1);
      }
      this.guardarCarrito();
    },
    guardarCarrito() {
      localStorage.setItem("carrito", JSON.stringify(this.carrito));
    },
  },
};
</script>

<template>
  <div>
    <Header />

    <main class="container my-5">
      <div class="row">
        <div class="col-md-8">
          <Articulos @add-to-cart="agregarAlCarrito" />
        </div>
        <div class="col-md-4">
          <Cart :carrito="carrito" @update-quantity="actualizarCantidad" />
        </div>
      </div>
    </main>
    <Footer />
  </div>
</template>

<style>
body {
  background-color: #f8f9fa;
}
</style>
