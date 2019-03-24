<template>
  <div id="app">
    <main>
      <Header :cart="cart"/>
      <div class="app-home">
        <Home @additem="onAddToCart($event)" @removeitem="onRemoveItem($event)"/>
      </div>
    </main>
  </div>
</template>

<script>
import Home from "./components/Home";
import Header from "./components/Header";

export default {
  name: "app",
  components: {
    Home,
    Header
  },
  data() {
    return {
      cart: []
    };
  },
  methods: {
    onAddToCart(item) {
      this.cart = this.cart.concat(item);
    },
    onRemoveItem(item) {
      this.cart = this.cart.filter(product => product.name !== item.name);
    }
  }
};
</script>

<style>
body,
html {
  margin: 0;
  padding: 0;
  font-family: "Muli", sans-serif;
  background-color: whitesmoke;
}
</style>
