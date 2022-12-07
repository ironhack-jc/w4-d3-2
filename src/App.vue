<template>
  <div>
    <AppHeader :count="numberOfItems" @refresh="fetchApi" />

    <div v-if="loading">Loading ....</div>
    <Cart v-else :items="items" />

    <!-- <app-footer /> -->
    <AppFooter :isMobile="!isDesktop" :submenu="menu" />
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import AppFooter from "./components/AppFooter.vue";
import Cart from "./components/Cart.vue";

const API_URL =
  "https://raw.githubusercontent.com/ironhack-jc/mid-term-api/main/cart";

export default {
  components: {
    AppHeader,
    AppFooter,
    Cart,
  },
  data() {
    return {
      loading: true,
      items: [],
      isDesktop: true,
      menu: ["Productos", "Servicios", "Contacta"],
    };
  },
  computed: {
    numberOfItems() {
      let sum = 0;

      for (const item of this.items) {
        sum += item.quantity;
      }

      return sum;
    },
  },
  methods: {
    async fetchApi(count) {
      console.log(count)

      this.loading = true;
      setTimeout(async () => {
        console.log("Loaded")

        const response = await fetch(API_URL);
        this.items = await response.json();
        this.loading = false;
      }, 3000)

    },

    validateForm() {
      alert(`Hola`);
    },
  },
  mounted() {
    this.fetchApi();
  },
};
</script>

<style scoped>
table {
  width: 100%;
}

table tfoot tr th {
  text-align: right;
}
</style>
