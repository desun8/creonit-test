<template>
  <div class="col-6">
    <div class="card">
      <div class="card__img-container  card-img-top">
        <img
            :src="image.url"
            :alt="image.name"
            class="card__img"
            loading="lazy"
        />
      </div>
      <div class="card__body  card-body">
        <h5 class="card__title  card-title">{{ title }}</h5>
        <h6 class="card__price  card-subtitle mb-2 text-muted">{{ price }} ₽</h6>
        <a v-for="color in colors" :key="color.id" :style="`--color: ${color.code}`" href="#"
           class="card__link   card-link">{{ color.title }}</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductCard",
  props: {
    id: Number,
    image: Object,
    title: String,
    price: Number,
    colors: Array
  }
};
</script>

<style>
.card {
  margin-bottom: 30px;
}
</style>
<style scoped>
.card {
  margin-bottom: 30px;
}

.card__img-container {
  position: relative;
  width: 100%;
  height: 0;
  padding: 50%;
  overflow: hidden;
}

.card__img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: contain;
}

.card__link {
  --color: #000;

  color: var(--color);
}
</style>