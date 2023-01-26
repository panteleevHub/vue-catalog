<template>
  <div class="sort">
    <p class="sort-caption">Сортировка:</p>
    <div class="sort-list">
      <button
        @click="onSortChange"
        value="price"
        class="sort-item"
        :class="{'sort-item-active': sort === 'price'}"
        type="button"
      >
        По цене
      </button>
      <button
        @click="onSortChange"
        value="sell"
        class="sort-item"
        :class="{'sort-item-active': sort === 'sell'}"
        type="button"
      >
        По популярности
      </button>
    </div>
    <div class="sort-buttons">
      <button
        @click="onSortDirectionChange"
        value="up"
        class="sort-button sort-button-up"
        :class="{'sort-button-active': direction === 'up'}"
        type="button"
        aria-label="По возрастанию"
      >
      </button>
      <button
        @click="onSortDirectionChange"
        value="down"
        class="sort-button sort-button-down"
        :class="{'sort-button-active': direction === 'down'}"
        type="button"
        aria-label="По убыванию"
      >
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    sort: String,
    direction: String
  },

  methods: {
    onSortChange({target}) {
      this.$emit('update:sort', target.value);
      target.blur();
    },

    onSortDirectionChange({target}) {
      this.$emit('update:direction', target.value);
      target.blur();
    }
  }
}
</script>

<style>
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
  padding-right: 217px;
}

.sort-item {
  font-size: 14px;
  line-height: 19px;
  font-weight: 400;
  padding: 0;
  color: var(--black-30);
  background-color: inherit;
  border: none;
  cursor: pointer;
}

.sort-item-active {
  pointer-events: none;
}

.sort-item:hover,
.sort-item:focus {
  color: var(--black-60);
}

.sort-item-active,
.sort-item-active:hover,
.sort-item:active {
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
  background-image: url("@/assets/img/icon-down.svg");
  border: none;
  opacity: 0.2;
  cursor: pointer;
}

.sort-button-up {
  transform: rotate(180deg);
}

.sort-button:hover,
.sort-button:focus {
  opacity: 0.4;
}

.sort-button-active,
.sort-button-active:hover,
.sort-button:active {
  opacity: 1;
}
</style>
