<template>
  <ul class="product-list">
		<ProductItem
      v-for="product in products"
      :product="product"
      :key="product.id"
    />
	</ul>
</template>

<script>
import ProductItem from './ProductItem.vue';

export default {
	props: {
		products: {
			type: Array,
			required: true
		}
	},
	components: {
		ProductItem,
	}
}
</script>

<style>
.product-list {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 48px 40px;
  padding: 0;
  margin: 0;
  margin-bottom: 40px;
  list-style: none;
}
</style>
