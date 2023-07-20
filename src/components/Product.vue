<template>
  <li
    @click="checked"
    :id="product.id"
    class="product"
    :class="product.check ? 'checked' : ''"
  >
    {{ product.title }}
  </li>
</template>

<script>
export default {
  props: {
    product: {
      type: Object,
      required: true,
    },
  },
  methods: {
    checked() {
      this.$emit('checked', this.product.id)
    },
  },
}
</script>

<style scoped>
.product {
  display: flex;
  gap: 20px;
  background: azure;
  padding: 15px;
  margin: 5px;
  border-radius: var(--br-4);
  border: var(--border);
  cursor: pointer;
}
.checked {
  color: gray;
  text-decoration: line-through;
  background: #e8e8e8;
}
</style>
