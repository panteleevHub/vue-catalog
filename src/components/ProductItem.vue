<template>
  <li class="product-item">
    <p class="product-image">
      <img :src="product.image" width="360" height="380" :alt="product.name">
    </p>
    <p class="product-info">
      <a class="product-name" href="#">{{ product.name }}</a>
      <span class="product-price">{{ product.price }} руб.</span>
      <span class="product-sell">Продано: {{ product.sell }} штук</span>
    </p>
    <p class="product-buttons">
      <a href="#" class="product-button product-button-cart button">В корзину</a>
      <a href="#" class="product-button product-button-comparison">Добавить к сравнению</a>
    </p>
  </li>
</template>

<script>
export default {
  props: {
    product: {
      type: Object,
      required: true
    }
  }
}
</script>

<style>
.product-item {
  position: relative;
}

.product-item-new::before {
  content: "";
  position: absolute;
  top: 29px;
  right: 27px;
  width: 62px;
  height: 62px;
  background-image: url("./assets/img/icon-new.svg");
}

.product-image {
  width: 360px;
  height: 380px;
  padding: 0;
  margin: 0;
  margin-bottom: 30px;
}

.product-info {
  display: grid;
  grid-template-columns: 2fr 1fr;
  row-gap: 10px;
  font-family: "Gilroy", "Arial", sans-serif;
  letter-spacing: 0.06em;
  margin: 0;
}

.product-name {
  font-size: 18px;
  line-height: 22px;
  font-weight: 800;
  color: var(--basic-black);
}

.product-price {
  font-size: 16px;
  line-height: 18px;
  padding-top: 3px;
  margin-right: -0.06em;
  text-align: right;
}

.product-buttons {
  display: none;
  position: absolute;
  top: 170px;
  left: 77px;
  margin: 0;
}

.product-item:hover .product-buttons,
.product-item:focus-within .product-buttons {
  display: block;
}

.product-button {
  display: block;
  width: 200px;
}

.product-button-cart {
  margin-bottom: 13px;
}

.product-button-comparison {
  font-size: 13px;
  line-height: 18px;
  text-align: center;
  letter-spacing: 0.1em;
  color: var(--basic-black);
  opacity: 0.5;
}

.product-button-comparison:hover,
.product-button-comparison:focus {
  opacity: 1;
}

.product-button-comparison:active {
  opacity: 0.2;
}
</style>
