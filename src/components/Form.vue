<template>
  <form @submit.prevent="addProduct" class="form">
    <label for="description">Название продукта</label>
    <input
      type="text"
      id="description"
      placeholder="Новый продукт..."
      v-model="title"
    />
    <button type="submit">Добавить продукт</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: '',
    }
  },
  methods: {
    addProduct() {
      if (this.title.trim() === '') {
        return (this.title = '')
      }
      const newProduct = {
        id: Date.now(),
        title: this.title,
        check: false,
      }
      this.$emit('create', newProduct)
      this.title = ''
    },
  },
}
</script>

<style scoped>
.form {
  display: grid;

  gap: 10px;

  background: aliceblue;
  padding: var(--pad-20);
  border-radius: var(--br-4);
  margin-bottom: 50px;
  font-size: 14px;
}

label {
  text-align: left;
  font-weight: var(--fw-500);
}

input,
button {
  font-size: 14px;
  font-family: inherit;
  padding: 5px;
  border-radius: var(--br-4);
  border: var(--border);
}

input {
  grid-column: 1/2;
  background: white;
}

button {
  height: 100%;
  align-self: flex-start;
  cursor: pointer;
  background: var(--bg-product);
  grid-row: 3;
}
@media screen and (min-width: 535px) {
  .form {
    grid-template: repeat(2, 1fr) / repeat(2, 1fr);
    row-gap: 0;
  }
  button {
    grid-row: 2;
    grid-column: 2;
  }
}
</style>
