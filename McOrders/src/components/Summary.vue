<template>
<!-- Componente que despliega la cantidad, total en base al producto, y total en base a todos los productos activos -->
  <section class="summary">
    <strong>Order Details</strong>
    <table>
      <thead>
        <tr>
          <th>Item</th>
          <th>Total</th>
        </tr>
      </thead>
      <tbody v-for="(product, n) in this.products" :key="n">
        <tr v-if="product.quantity > 0">
          <td>{{ product.quantity }}x {{ product.name }}</td>
          <td>${{ (product.quantity * product.price).toFixed(2) }}</td>
        </tr>
      </tbody>
      <tr>
        <th>Total</th>
        <!-- Cada vez que se modifica algo en el componente, se refresca, se manda a llamar el componente, por eso se manda a llamar varias veces el getTotal -->
        <th>${{getTotal(this.products)}}</th>
      </tr>
    </table>
  </section>
</template>

<script>
export default {
  props: {
    products: {
      type: Array,
    },
  },

  methods: {
    getTotal(products) {
      let total = 0;
      for (let item of products) {
        total = total + item.price * item.quantity;
      }

      return total.toFixed(2);
    },
  },
};
</script>

<style></style>
