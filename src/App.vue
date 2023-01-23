<template>
  <div class="catalog">
    <div class="wrapper">
        <h1 class="catalog-title title">Моноподы для селфи</h1>
        <ul class="breadcrumbs">
          <li class="breadcrumbs-item">
            <a href="index.html">Главная</a>
          </li>
          <li class="breadcrumbs-item">
            <a href="#">Каталог товаров</a>
          </li>
          <li class="breadcrumbs-item breadcrumbs-item-current">
            <a href="#">Моноподы для селфи</a>
          </li>
        </ul>
      </div>
    <div class="catalog-header">
      <div class="wrapper catalog-header-container">
        <p class="catalog-filter-caption">Фильтр:</p>
        <div class="sort">
          <p class="sort-caption">Сортировка:</p>
          <ul class="sort-list">
            <li class="sort-item sort-item-current">
              <a href="">По цене</a>
            </li>
            <li class="sort-item">
              <a href="">По типу</a>
            </li>
            <li class="sort-item">
              <a href="">По популярности</a>
            </li>
          </ul>
          <div class="sort-buttons">
            <button class="sort-button sort-button-up" type="button" aria-label="Назад"></button>
            <button class="sort-button sort-button-down sort-button-active" type="button" aria-label="Вперед"></button>
          </div>
        </div>
      </div>
    </div>
    <div class="catalog-content">
      <div class="wrapper catalog-content-container">
        <section class="filter">
          <h2 class="visually-hidden">Фильтр товаров</h2>
          <Filter @changeFilter="onFilterChange" />
        </section>
        <section class="products">
          <h2 class="visually-hidden">Список товаров</h2>
          <div v-if="!isProductListEmpty">
            <ProductList :products="filteredProducts" />
            <ProductPagination :pages="pages" :currentPage="currentPage" />
          </div>
          <p v-else class="products-message">Нет товаров</p>
        </section>
      </div>
    </div>
  </div>
</template>

<script>
import monopodAmateur from './assets/img/monopod-amateur.jpg';
import monopodPro from './assets/img/monopod-pro.jpg';
import monopodUnsinkable from './assets/img/monopod-unsinkable.jpg';
import monopodFollowMe from './assets/img/monopod-follow-me.jpg';
import ProductList from './components/ProductList.vue';
import ProductPagination from './components/ProductPagination.vue';
import Filter from './components/Filter.vue';

export default {
  data() {
    return {
      products: [
        {
          id: 1,
          name: 'Любительская селфи-палка',
          price: 1100,
          image: monopodAmateur,
          color: 'black',
          bluetooth: false
        },
        {
          id: 2,
          name: 'Профессиональная селфи-палка',
          price: 1500,
          image: monopodPro,
          color: 'black',
          bluetooth: true
        },
        {
          id: 3,
          name: 'Непотопляемая селфи-палка',
          price: 1500,
          image: monopodUnsinkable,
          color: 'black',
          bluetooth: false
        },
        {
          id: 4,
          name: 'Селфи-палка «Следуй за мной»',
          price: 1900,
          image: monopodFollowMe,
          color: 'black',
          bluetooth: false
        }
      ],
      selectedFilterItems: {
        minPrice: 0,
        maxPrice: 10000,
        checkedColors: ['black'],
        bluetooth: true
      },
      pages: 3,
      currentPage: 1
    }
  },

  computed: {
    filteredProducts() {
      return this.products.filter((product) => {
        return product.price >= this.selectedFilterItems.minPrice &&
          product.price <= this.selectedFilterItems.maxPrice &&
          this.selectedFilterItems.checkedColors.includes(product.color) &&
          this.selectedFilterItems.bluetooth === product.bluetooth;
      });
    },

    isProductListEmpty() {
      return this.filteredProducts.length === 0;
    }
  },

  methods: {
    onFilterChange(data) {
      this.selectedFilterItems = {
        minPrice: data.minPrice,
        maxPrice: data.maxPrice,
        checkedColors: data.checkedColors,
        bluetooth: data.bluetooth
      };
    }
  },

  components: {
    ProductList,
    ProductPagination,
    Filter
  }
}
</script>

<style>
.catalog {
  padding-top: 43px;
}

.catalog-title {
  padding: 0 60px;
  margin: 0;
}

.catalog-header {
  background: linear-gradient(90deg, var(--special-grey-light) calc(50% - 252px), var(--basic-grey-light) calc(50% - 252px));
}

.catalog-header-container {
  display: flex;
  padding-top: 25px;
  padding-bottom: 25px;
}

.catalog-filter-caption {
  width: 328px;
  font-family: "Gilroy", "Arial", sans-serif;
  font-size: 16px;
  line-height: 20px;
  font-weight: 800;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  padding: 0 60px;
  margin: 0;
}

.catalog-content {
  background: linear-gradient(90deg, var(--basic-grey-light) calc(50% - 252px), transparent calc(50% - 252px));
  padding: 70px 0;
  padding-bottom: 78px;
}

.catalog-content-container {
  display: grid;
  grid-template-columns: 328px 1fr;
  column-gap: 72px;
}

.products-message {
  font-size: 34px;
  text-align: center;
}

.breadcrumbs {
  display: flex;
  flex-wrap: wrap;
  gap: 10px 14px;
  padding: 0;
  padding: 30px 60px 50px;
  margin: 0;
  list-style: none;
}

.breadcrumbs-item {
  position: relative;
  padding-right: 26px;
}

.breadcrumbs-item:not(:last-child):after {
  content: "";
  position: absolute;
  top: 50%;
  right: 0;
  transform: translateY(-50%);
  width: 12px;
  height: 12px;
  background-image: url("./assets/img/icon-arrow.svg");
}

.breadcrumbs-item a {
  font-size: 14px;
  line-height: 19px;
  color: var(--black-30);
}

.breadcrumbs-item-current {
  pointer-events: none;
  cursor: default;
}

.breadcrumbs-item:not(.breadcrumbs-item-current) a:hover,
.breadcrumbs-item:not(.breadcrumbs-item-current) a:focus {
  color: var(--black-60);
}

.breadcrumbs-item:not(.breadcrumbs-item-current) a:active {
  color: var(--black-10);
}

.sort {
  display: flex;
}

.sort-caption {
  max-width: 350px;
  font-family: "Gilroy", "Arial", sans-serif;
  font-size: 16px;
  line-height: 20px;
  font-weight: 800;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  margin: 0;
  padding-left: 72px;
  padding-right: 74px;
}

.sort-list {
  display: flex;
  flex-wrap: wrap;
  gap: 10px 30px;
  width: 507px;
  padding: 0;
  padding-right: 217px;
  margin: 0;
  list-style: none;
}

.sort-item a {
  font-size: 14px;
  line-height: 19px;
  font-weight: 400;
  color: var(--black-30);
}

.sort-item-current a {
  pointer-events: none;
  cursor: default;
}

.sort-item a:hover,
.sort-item a:focus {
  color: var(--black-60);
}

.sort-item-current a,
.sort-item-current a:hover,
.sort-item a:active {
  color: var(--basic-black);
}

.sort-buttons {
  display: flex;
  justify-content: space-between;
  width: 52px;
}

.sort-button {
  width: 18px;
  height: 18px;
  padding: 0;
  background-color: transparent;
  background-image: url("./assets/img/icon-down.svg");
  border: none;
  opacity: 0.2;
  cursor: pointer;
}

.sort-button-active {
  opacity: 1;
}

.sort-button-up {
  transform: rotate(180deg);
}

.sort-button:hover,
.sort-button:focus {
  opacity: 0.4;
}

.sort-button:active {
  opacity: 1;
}

.filter {
  padding: 0 60px;
  padding-right: 68px;
}
</style>
