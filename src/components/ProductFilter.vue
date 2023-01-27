<template>
  <form @submit.prevent="onFormSubmit" class="filter-form">
    <fieldset class="filter-fieldset filter-price">
      <legend>Стоимость</legend>
      <div class="range-selected-bar" :style="rangeBarStyle"></div>
      <div class="range-controls">
        <input
          type="range"
          :min="range.min"
          :max="range.max"
          :step="range.step"
          :value="filterData.minPrice"
          @input="onMinPriceChange"
        >
        <input
          type="range"
          :min="range.min"
          :max="range.max"
          :step="range.step"
          :value="filterData.maxPrice"
          @input="onMaxPriceChange"
        >
      </div>
      <div class="price-controls">
        <p class="price min-price">от {{ filterData.minPrice }}</p>
        <p class="price max-price">до {{ filterData.maxPrice }}</p>
      </div>
    </fieldset>
    <fieldset class="filter-fieldset filter-color">
      <legend>Цвет</legend>
      <span v-if="!isColorChecked" class="filter-color-message">Выберите цвет</span>
      <ul class="filter-color-list">
        <li class="filter-color-item">
          <input
            v-model="filterData.checkedColors"
            class="visually-hidden filter-color-input"
            type="checkbox"
            value="all"
            id="all-colors"
          >
          <label class="filter-color-label" for="all-colors">Все</label>
        </li>
        <li class="filter-color-item">
          <input
            v-model="filterData.checkedColors"
            class="visually-hidden filter-color-input"
            type="checkbox"
            value="black"
            id="color-black"
          >
          <label class="filter-color-label" for="color-black">Чёрный</label>
        </li>
        <li class="filter-color-item">
          <input
            v-model="filterData.checkedColors"
            class="visually-hidden filter-color-input"
            type="checkbox"
            value="white"
            id="color-white"
          >
          <label class="filter-color-label" for="color-white">Белый</label>
        </li>
        <li class="filter-color-item">
          <input
            v-model="filterData.checkedColors"
            class="visually-hidden filter-color-input"
            type="checkbox"
            value="blue"
            id="color-blue"
          >
          <label class="filter-color-label" for="color-blue">Синий</label>
        </li>
        <li class="filter-color-item">
          <input
            v-model="filterData.checkedColors"
            class="visually-hidden filter-color-input"
            type="checkbox"
            value="red"
            id="color-red"
          >
          <label class="filter-color-label" for="color-red">Красный</label>
        </li>
        <li class="filter-color-item">
          <input
            v-model="filterData.checkedColors"
            class="visually-hidden filter-color-input"
            type="checkbox"
            value="pink"
            id="color-pink"
          >
          <label class="filter-color-label" for="color-pink">Розовый</label>
        </li>
      </ul>
    </fieldset>
    <fieldset class="filter-fieldset filter-bluetooth">
      <legend>Bluetooth</legend>
      <ul class="filter-bluetooth-list">
        <li class="filter-bluetooth-item">
          <input v-model="filterData.bluetooth" class="visually-hidden filter-bluetooth-input" type="radio" value="all" id="bluetooth-all">
          <label class="filter-bluetooth-label" for="bluetooth-all">Все</label>
        </li>
        <li class="filter-bluetooth-item">
          <input v-model="filterData.bluetooth" class="visually-hidden filter-bluetooth-input" type="radio" :value="true" id="bluetooth-yes">
          <label class="filter-bluetooth-label" for="bluetooth-yes">Есть</label>
        </li>
        <li class="filter-bluetooth-item">
          <input v-model="filterData.bluetooth" class="visually-hidden filter-bluetooth-input" type="radio" :value="false" id="bluetooth-no">
          <label class="filter-bluetooth-label" for="bluetooth-no">Нет</label>
        </li>
      </ul>
    </fieldset>
    <button
      ref="submitButton"
      class="filter-submit button"
      type="submit"
    >
      Показать
    </button>
    <button
      @click="onResetButtonClick"
      class="filter-reset"
      type="button"
    >
      Сбросить фильтр
    </button>
  </form>
</template>

<script>
export default {
  props: {
    filterOptions: {
      type: Object
    }
  },

  mounted() {
    this.initialFilterOptions = {...this.filterOptions};
  },

  data() {
    return {
      range: {
        min: 0,
        max: 10000,
        step: 1000
      },
      filterData: {
        minPrice: this.filterOptions.minPrice,
        maxPrice: this.filterOptions.maxPrice,
        checkedColors: this.filterOptions.checkedColors,
        bluetooth: this.filterOptions.bluetooth,
      },
      initialFilterOptions: {},
      isColorChecked: true
    }
  },

  computed: {
    rangeBarStyle() {
      return {
        left: `${this.filterData.minPrice / this.range.max * 100}%`,
        right: `${100 - (this.filterData.maxPrice / this.range.max * 100)}%`,
      };
    }
  },

  methods: {
    onFormSubmit() {
      this.$refs.submitButton.blur();

      if (this.filterData.checkedColors.length === 0) {
        this.isColorChecked = false;
        return;
      }

      this.isColorChecked = true;

      this.$emit('update:filterOptions', {
        ...this.filterData
      });
    },

    onMinPriceChange({target}) {
      this.filterData.minPrice = parseInt(target.value);
      if (this.filterData.minPrice >= this.filterData.maxPrice) {
        this.filterData.minPrice = this.filterData.maxPrice - this.range.step;
      }
    },

    onMaxPriceChange({target}) {
      this.filterData.maxPrice = parseInt(target.value);
      if (this.filterData.maxPrice <= this.filterData.minPrice) {
        this.filterData.maxPrice = this.filterData.minPrice + this.range.step;
      }
    },

    onResetButtonClick() {
      this.filterData = {...this.initialFilterOptions};

      this.$emit('update:filterOptions', {
        ...this.initialFilterOptions
      });
    }
  }
}
</script>

<style>
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
  padding: 40px 0;
  padding-bottom: 38px;
}

.range-selected-bar {
  position: absolute;
  left: 0;
  right: 0;
  height: 2px;
  background-color: var(--special-green);
  z-index: 2;
}

.range-controls {
  position: relative;
  width: 100%;
  height: 20px;
  margin-bottom: 8px;
}

.range-controls input[type="range"] {
  appearance: none;
  width: 100%;
  height: 2px;
  position: absolute;
  top: 0;
  left: 0;
  background-color: var(--black-20);
  margin: 0;
}

.range-controls input[type="range"]::-webkit-slider-thumb {
  appearance: none;
  z-index: 3;
  position: relative;
  width: 20px;
  height: 20px;
  background-color: var(--special-grey);
  border: 8px solid var(--basic-white);
  border-radius: 50%;
  box-shadow: 0px 2px 2px var(--black-20);
  cursor: pointer;
}

.price-controls {
  display: flex;
  justify-content: space-between;
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

.filter-color-message {
  display: block;
  padding-bottom: 20px;
  color: var(--basic-red);
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
  background-image: url("@/assets/img/icon-check.svg");
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
  margin-bottom: 20px;
}

.filter-reset {
  width: 100%;
  font-size: 16px;
  letter-spacing: 0.04em;
  padding: 0;
  border: none;
  background-color: inherit;
  cursor: pointer;
}

.filter-reset:hover {
  text-decoration: underline;
}
</style>
