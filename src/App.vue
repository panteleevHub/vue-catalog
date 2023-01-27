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
        <ProductSort
          v-model:sort="sort.value"
          v-model:direction="sort.direction"
        />
      </div>
    </div>
    <div class="catalog-content">
      <div class="wrapper catalog-content-container">
        <section class="filter">
          <h2 class="visually-hidden">Фильтр товаров</h2>
          <ProductFilter v-model:filterOptions="filterOptions" />
        </section>
        <section class="products">
          <h2 class="visually-hidden">Список товаров</h2>
          <div v-if="!isProductListEmpty">
            <ProductList :products="sortedProducts" />
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
import ProductFilter from './components/ProductFilter.vue';
import ProductSort from './components/ProductSort.vue';

export default {
  data() {
    return {
      products: [
        {
          id: 1,
          name: 'Любительская селфи-палка',
          price: 1100,
          sell: 2500,
          image: monopodAmateur,
          color: 'black',
          bluetooth: false
        },
        {
          id: 2,
          name: 'Профессиональная селфи-палка',
          price: 1500,
          sell: 2000,
          image: monopodPro,
          color: 'black',
          bluetooth: true
        },
        {
          id: 3,
          name: 'Непотопляемая селфи-палка',
          price: 1500,
          sell: 500,
          image: monopodUnsinkable,
          color: 'black',
          bluetooth: false
        },
        {
          id: 4,
          name: 'Селфи-палка «Следуй за мной»',
          price: 1900,
          sell: 1300,
          image: monopodFollowMe,
          color: 'black',
          bluetooth: false
        },
        {
          id: 5,
          name: 'Розовая селфи-палка',
          price: 800,
          sell: 1700,
          image: monopodAmateur,
          color: 'pink',
          bluetooth: false
        },
        {
          id: 6,
          name: 'Красная селфи-палка',
          price: 2500,
          sell: 825,
          image: monopodUnsinkable,
          color: 'red',
          bluetooth: true
        },
        {
          id: 7,
          name: 'Профессиональная селфи-палка',
          price: 1500,
          sell: 2700,
          image: monopodPro,
          color: 'white',
          bluetooth: true
        },
        {
          id: 8,
          name: 'Профессиональная селфи-палка',
          price: 10000,
          sell: 1200,
          image: monopodUnsinkable,
          color: 'red',
          bluetooth: true
        },
        {
          id: 9,
          name: 'Cиняя селфи палка',
          price: 5000,
          sell: 556,
          image: monopodFollowMe,
          color: 'blue',
          bluetooth: true
        },
        {
          id: 10,
          name: 'Белая селфи-палка',
          price: 1000,
          sell: 1005,
          image: monopodPro,
          color: 'white',
          bluetooth: false
        }
      ],
      filterOptions: {
        minPrice: 0,
        maxPrice: 10000,
        checkedColors: ['all'],
        bluetooth: 'all'
      },
      sort: {
        value: 'price',
        direction: 'up'
      },
      pages: 3,
      currentPage: 1
    }
  },

  computed: {
    filteredProducts() {
      return this.products.filter((product) => {
        return product.price >= this.filterOptions.minPrice &&
          product.price <= this.filterOptions.maxPrice &&
          (this.filterOptions.checkedColors.includes(product.color) ||
          this.filterOptions.checkedColors.includes('all')) &&
          (this.filterOptions.bluetooth === product.bluetooth ||
          this.filterOptions.bluetooth === 'all');
      });
    },

    sortedProducts() {
      if (this.sort.direction === 'up') {
        return [...this.filteredProducts].sort((productA, productB) => {
          return productA[this.sort.value] - productB[this.sort.value];
        });
      }

      return [...this.filteredProducts].sort((productA, productB) => {
          return productB[this.sort.value] - productA[this.sort.value];
        });
    },

    isProductListEmpty() {
      return this.filteredProducts.length === 0;
    }
  },

  methods: {
    onFilterChange(data) {
      this.filterOptions = {...data};
    }
  },

  components: {
    ProductList,
    ProductPagination,
    ProductFilter,
    ProductSort
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

.filter {
  padding: 0 60px;
  padding-right: 68px;
}
</style>
