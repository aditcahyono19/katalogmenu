<template>
  <div class="menu">
    <Navbar />
    <div class="container">
      <div class="row mt-4">
        <div class="col">
          <h2>Daftar <strong> Makanan </strong></h2>
        </div>
      </div>
      <div class="row mt-3">
        <div class="col">
          <div class="input-group mb-3">
            <input
            v-model="search"
              type="text"
              class="form-control"
              placeholder="Cari Makanan Kesukaan Anda ..."
              aria-label="Cari"
              aria-describedby="basic-addon1"
              @keyup="searchMenu"
            />
            <div class="input-group-prepend">
            <span class="input-group-text" id="basic-addon1"><b-icon-search></b-icon-search>
            </span>
          </div>
        </div>
        </div>
      </div>
      <div class="row mb-4">
        <div
          class="col-md-4 mt-4"
          v-for="product in products"
          :key="product.id"
        >
          <CardProducts :product="product" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import CardProducts from "@/components/CardProducts.vue";
import axios from "axios";
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Menu",
  components: {
    Navbar,
    CardProducts,
  },
  data() {
    return {
      products: [],
      search: '',
    };
  },
  methods: {
    setProduct(data) {
      this.products = data;
    },
    searchMenu () {
      axios
      .get(
        "https://my-json-server.typicode.com/aditcahyono19/katalogmenu/products?q="+this.search
      )
      .then((response) => this.setProduct(response.data))
      .catch((error) => console.log(error));
    }
  },
  mounted() {
    axios
      .get(
        "https://my-json-server.typicode.com/aditcahyono19/katalogmenu/products"
      )
      .then((response) => this.setProduct(response.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style></style>
