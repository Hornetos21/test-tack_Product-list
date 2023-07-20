<template>
  <div class="wrapper">
    <h2 class="title">Список продуктов</h2>
    <ul class="list">
      <Product
        v-for="product in products"
        :product="product"
        :key="product.id"
        @checked="toggle"
      />
    </ul>
  </div>
</template>

<script>
import Product from '@/components/Product.vue'

export default {
  components: { Product },
  props: {
    products: {
      type: Array,
      required: true,
    },
    toggle: {
      type: Function,
      required: true,
    },
  },
}
</script>

<style scoped>
.wrapper {
  padding: var(--pad-20);
  background: var(--bg-primary);
  border-radius: var(--br-4);
}

.list {
  padding: 0;
  list-style: none;
}

.title {
  font-size: 22px;
  font-weight: var(--fw-500);
  margin-bottom: 20px;
}
</style>