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
          <form class="filter-form" method="POST" target="_blank">
            <fieldset class="filter-fieldset filter-price">
              <legend>Стоимость</legend>
              <div class="range-controls">
                <div class="scale">
                  <div class="bar"></div>
                </div>
                <button class="toggle toggle-min" type="button"></button>
                <button class="toggle toggle-max" type="button"></button>
              </div>
              <div class="price-controls">
                <p class="price min-price">от 0</p>
                <p class="price max-price">до 5000</p>
              </div>
            </fieldset>
            <fieldset class="filter-fieldset filter-color">
              <legend>Цвет</legend>
              <ul class="filter-color-list">
                <li class="filter-color-item">
                  <input class="visually-hidden filter-color-input" type="checkbox" name="black" id="color-black" checked>
                  <label class="filter-color-label" for="color-black">Чёрный</label>
                </li>
                <li class="filter-color-item">
                  <input class="visually-hidden filter-color-input" type="checkbox" name="white" id="color-white">
                  <label class="filter-color-label" for="color-white">Белый</label>
                </li>
                <li class="filter-color-item">
                  <input class="visually-hidden filter-color-input" type="checkbox" name="blue" id="color-blue" checked>
                  <label class="filter-color-label" for="color-blue">Синий</label>
                </li>
                <li class="filter-color-item">
                  <input class="visually-hidden filter-color-input" type="checkbox" name="red" id="color-red" checked>
                  <label class="filter-color-label" for="color-red">Красный</label>
                </li>
                <li class="filter-color-item">
                  <input class="visually-hidden filter-color-input" type="checkbox" name="pink" id="color-pink">
                  <label class="filter-color-label" for="color-pink">Розовый</label>
                </li>
              </ul>
            </fieldset>
            <fieldset class="filter-fieldset filter-bluetooth">
              <legend>Bluetooth</legend>
              <ul class="filter-bluetooth-list">
                <li class="filter-bluetooth-item">
                  <input class="visually-hidden filter-bluetooth-input" type="radio" name="bluetooth" value="yes" id="bluetooth-yes" checked>
                  <label class="filter-bluetooth-label" for="bluetooth-yes">Есть</label>
                </li>
                <li class="filter-bluetooth-item">
                  <input class="visually-hidden filter-bluetooth-input" type="radio" name="bluetooth" value="no" id="bluetooth-no">
                  <label class="filter-bluetooth-label" for="bluetooth-no">Нет</label>
                </li>
              </ul>
            </fieldset>
            <button class="filter-submit button" type="submit">Показать</button>
          </form>
        </section>
        <section class="products">
          <h2 class="visually-hidden">Список товаров</h2>
          <ul class="product-list">
            <li v-for="product in products" class="product-item">
              <p class="product-image">
                <img :src="product.image" width="360" height="380" :alt="product.name">
              </p>
              <p class="product-info">
                <a class="product-name" href="#">{{ product.name }}</a>
                <span class="product-price">{{ product.price }} руб.</span>
              </p>
              <p class="product-buttons">
                <a href="#" class="product-button product-button-cart button">В корзину</a>
                <a href="#" class="product-button product-button-comparison">Добавить к сравнению</a>
              </p>
            </li>
          </ul>
          <ul class="pagination">
            <li class="pagination-item">
              <a class="pagination-toggle pagination-toggle-previous" href="#">Назад</a>
            </li>
            <li class="pagination-item">
              <ul class="pages-list">
                <li class="pages-item pages-item-current">
                  <a href="#">1</a>
                </li>
                <li class="pages-item">
                  <a href="#">2</a>
                </li>
                <li class="pages-item">
                  <a href="#">3</a>
                </li>
              </ul>
            </li>
            <li class="pagination-item">
              <a class="pagination-toggle pagination-toggle-next" href="#">Вперед</a>
            </li>
          </ul>
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

export default {
  data() {
    return {
      products: [
        {
          name: 'Любительская селфи-палка',
          price: '1 100',
          image: monopodAmateur
        },
        {
          name: 'Профессиональная селфи-палка',
          price: '1 500',
          image: monopodPro
        },
        {
          name: 'Непотопляемая селфи-палка',
          price: '1 500',
          image: monopodUnsinkable
        },
        {
          name: 'Селфи-палка «Следуй за мной»',
          price: '1 900',
          image: monopodFollowMe
        }
      ]
    }
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

.filter legend {
  font-family: "Gilroy", "Arial", sans-serif;
  font-size: 14px;
  line-height: 17px;
  font-weight: 800;
  letter-spacing: 0.1em;
  padding-top: 16px;
}

.filter-fieldset {
  position: relative;
  padding: 0;
  margin: 0;
  border: none;
}

.filter-fieldset::before {
  content: "";
  position: absolute;
  top: -33px;
  left: 0;
  width: 100%;
  height: 2px;
  background-color: var(--basic-black);
}

/* Filter price */

.filter-price {
  padding: 30px 0;
  padding-bottom: 38px;
}

.range-controls {
  position: relative;
  width: 100%;
  height: 20px;
  padding: 9px 0;
  margin-bottom: 8px;
}

.range-controls .scale {
  width: 100%;
  height: 2px;
  padding: 0 10px;
  background-color: var(--black-20);
}

.range-controls .bar {
  width: 114px;
  height: 2px;
  background-color: var(--special-green);
}

.range-controls .toggle {
  position: absolute;
  top: 0;
  width: 20px;
  height: 20px;
  padding: 0;
  background-color: var(--special-grey);
  border: 8px solid var(--basic-white);
  border-radius: 50%;
  box-shadow: 0px 2px 2px var(--black-20);
  cursor: pointer;
}

.range-controls .toggle-min {
  left: 0;
}

.range-controls .toggle-max {
  right: 66px;
}

.price-controls {
  display: flex;
  column-gap: 70px;
}

.price-controls .price {
  font-family: "Gilroy", "Arial", sans-serif;
  font-size: 14px;
  line-height: 16px;
  margin: 0;
}

/* Filter color and bluetooth */

.filter-color {
  padding-top: 30px;
  padding-bottom: 39px;
}

.filter-bluetooth {
  padding-top: 28px;
  padding-bottom: 41px;
}

.filter-color-list,
.filter-bluetooth-list {
  padding: 0;
  margin: 0;
  list-style: none;
}

.filter-color-item {
  margin-bottom: 15px;
}

.filter-bluetooth-item {
  margin-bottom: 16px;
}

.filter-color-item:last-child,
.filter-bluetooth-item:last-child {
  margin-bottom: 0;
}

.filter-color-input + label::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 24px;
  height: 24px;
  border: 2px solid var(--basic-black);
  border-radius: 2px;
}

.filter-color-input:checked + label::after {
  content: "";
  position: absolute;
  top: 2px;
  left: 2px;
  width: 21px;
  height: 21px;
  background-image: url("./assets/img/icon-check.svg");
}

.filter-bluetooth-input + label::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 24px;
  height: 24px;
  border: 2px solid var(--basic-black);
  border-radius: 50%;
}

.filter-bluetooth-input:checked + label::after {
  content: "";
  position: absolute;
  top: 8px;
  left: 8px;
  width: 8px;
  height: 8px;
  background-color: var(--basic-black);
  border-radius: 50%;
}

.filter-color-input:hover + label::before,
.filter-bluetooth-input:hover + label::before,
.filter-color-input:hover + label::after,
.filter-bluetooth-input:hover + label::after,
.filter-color-input:focus + label::before,
.filter-bluetooth-input:focus + label::before,
.filter-color-input:focus + label::after,
.filter-bluetooth-input:focus + label::after {
  opacity: 0.6;
}

.filter-color-input:active + label::before,
.filter-bluetooth-input:active + label::before,
.filter-color-input:active + label::after,
.filter-bluetooth-input:active + label::after {
  opacity: 1;
}

.filter-color-input:disabled + label::before,
.filter-bluetooth-input:disabled + label::before,
.filter-color-input:disabled + label::after,
.filter-bluetooth-input:disabled + label::after {
  opacity: 0.25;
}

.filter-color-input:disabled + label,
.filter-bluetooth-input:disabled + label {
  cursor: default;
}

.filter-color-label,
.filter-bluetooth-label {
  position: relative;
  display: flex;
  align-items: center;
  font-size: 14px;
  line-height: 19px;
  min-height: 24px;
  cursor: pointer;
}

.filter-color-label {
  padding-left: 42px;
}

.filter-bluetooth-label {
  padding-left: 40px;
}

.filter-submit {
  width: 100%;
  padding-right: 14px;
}

/* Products */

.product-list {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 48px 40px;
  padding: 0;
  margin: 0;
  margin-bottom: 40px;
  list-style: none;
}

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
  display: flex;
  justify-content: space-between;
  font-family: "Gilroy", "Arial", sans-serif;
  letter-spacing: 0.06em;
  margin: 0;
}

.product-name {
  width: 265px;
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

/* Pagination */

.pagination {
  display: flex;
  justify-content: space-between;
  align-items: center;
  column-gap: 20px;
  font-family: "Gilroy", "Arial", sans-serif;
  font-size: 16px;
  line-height: 20px;
  font-weight: 800;
  background-color: var(--basic-grey-light);
  padding: 0;
  margin: 0;
  list-style: none;
}

.pages-list {
  display: flex;
  flex-wrap: wrap;
  gap: 10px 30px;
  padding: 0;
  margin: 0;
  list-style: none;
}

.pages-item a {
  color: var(--black-30);
}

.pages-item-current a {
  pointer-events: none;
  cursor: default;
}

.pages-item a:hover,
.pages-item a:focus {
  color: var(--black-60);
}

.pages-item-current a,
.pages-item-current a:hover,
.pages-item a:active {
  color: var(--basic-black);
}

.pagination-toggle {
  display: block;
  max-width: 180px;
  text-transform: uppercase;
  text-align: center;
  letter-spacing: 0.1em;
  margin-right: -0.1em;
  padding: 25px 30px;
  color: var(--basic-black);
}

.pagination-toggle:hover,
.pagination-toggle:focus {
  background-color: var(--special-grey-light);
}

.pagination-toggle:active {
  color: var(--black-30);
}
</style>
