<template>
  <div class="row">
    <div class="col-6">
      <div class="card">
        <img
            src="http://placehold.it/200x200"
            class="card-img-top"
            alt="Название"
        />
        <div class="card-body">
          <h5 class="card-title">Детский трюковой самокат Razor Grom</h5>
          <h6 class="card-subtitle mb-2 text-muted">4 990 ₽</h6>
          <a href="#" class="card-link" style="color: blue">Синий</a>
          <a href="#" class="card-link" style="color: green">Зелёный</a>
        </div>
      </div>
    </div>
    <div class="col-6">
      <div class="card">
        <img
            src="http://placehold.it/200x200"
            class="card-img-top"
            alt="Название"
        />
        <div class="card-body">
          <h5 class="card-title">Детский самокат Razor</h5>
          <h6 class="card-subtitle mb-2 text-muted">5 990 ₽</h6>
          <a href="#" class="card-link" style="color: blue">Синий</a>
        </div>
      </div>
    </div>

    <ProductCard
        v-for="item in items"
        :key="item.id"
        :image="item.image.file"
        :title="item.title"
        :price="item.price"
        :colors="item.colors"
    />
  </div>
</template>

<script>
import axios from "axios";
import ProductCard from "@/Products/ProductCard";

export default {
  name: "ProductsList",
  components: { ProductCard },
  data() {
    return {
      items: undefined
    };
  },
  methods: {
    async getData() {
      const res = await axios.get("https://vue-study.dev.creonit.ru/api/products?categoryId=3");
      this.items = res.data.items;
    }
  },
  mounted() {
    this.getData();
  }
};
</script>
