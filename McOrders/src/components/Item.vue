<template>
<!-- Componente encargado de recibir un producto y desplegar sus datos.
Sus metodos aumentan o decrementan la propiedad quantity del elemento, y activan o desactivan su propiedad active -->
  <div @click="itemSelected()" :class="this.isSelected">
    <div class="photo">
      <img :src="this.item.photo" />
    </div>
    <div class="description">
      <span class="name">{{ this.item.name }}</span>
      <span class="price">${{ this.item.price }}</span>
      <div class="quantity-area">
        <button @click.stop="count(false)">-</button>
        <span class="quantity">{{ this.item.quantity }}</span>
        <button @click.stop="count(true)">+</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
    },
  },

  data() {
    return {
      itemCount: 0,
      isSelected: "product",
    };
  },

  methods: {
    itemSelected() {
      this.item.active = !this.item.active;   /*Toogle state */
      if (this.item.active === true)          /* Si lo selecciono, aplica estilo */
        this.isSelected = "product selected";
      else this.isSelected = "product";
    },

    count(direction) {          /* Direccion: - <---|---> + */
      if (this.item.active) {   
        if (direction) 
            this.item.quantity++;
        else {
          if (this.item.quantity > 0) 
            this.item.quantity--;
        }
      }
    },
  },
};
</script>

<style>

</style>
