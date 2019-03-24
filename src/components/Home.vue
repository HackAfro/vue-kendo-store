<template>
  <div class="main">
    <section class="banners">
      <div v-for="banner in banners" :key="banner.src">
        <img :src="banner.src" :alt="banner.alt">
      </div>
    </section>
    <section class="product-area">
      <ProductList
        :products="products"
        @additem="onAddToCart($event)"
        @removeitem="onRemoveItem($event)"
      />
    </section>
  </div>
</template>

<script>
import ProductList from "./ProductList";

export default {
  name: "Home",
  components: {
    ProductList
  },
  data() {
    return {
      products: [],
      banners: [
        {
          src:
            "https://images.pexels.com/photos/1633525/pexels-photo-1633525.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=3000&w=510",
          alt: "A tasty treat"
        },
        {
          src:
            "https://images.pexels.com/photos/940302/pexels-photo-940302.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=300&w=510",
          alt: "Chocolate covered pancakes"
        },
        {
          src:
            "https://images.pexels.com/photos/928475/pexels-photo-928475.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=300&w=510",
          alt: "Burger and fries"
        },
        {
          src:
            "https://images.pexels.com/photos/459469/pexels-photo-459469.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=300&w=510",
          alt: "Get ready to slice"
        }
      ]
    };
  },
  methods: {
    onAddToCart(item) {
      console.log(item)
      this.$emit("additem", item);
    },
    onRemoveItem(item) {
      this.$emit("removeitem", item);
    }
  },
  async mounted() {
    const res = await fetch("http://localhost:4000/products");
    const products = await res.json();

    this.products = products;
  }
};
</script>

<style lang="scss" scoped>
.main {
  width: 90%;
  margin: auto;
  padding: 20px 15px;
  margin-top: 30px;

  .banners {
    display: flex;
    align-items: center;
    justify-content: center;

    div {
      width: 26%;
      margin-right: 10px;
      img {
        height: 200px;
        width: 100%;
        max-width: 100%;
        border-radius: 10px;
        object-fit: cover;
      }
    }
  }
}
</style>
