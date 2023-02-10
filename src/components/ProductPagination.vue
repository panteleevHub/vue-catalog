<template>
  <ul class="pagination">
    <li class="pagination-item">
      <button
        @click="onPrevButtonClick"
        class="pagination-toggle pagination-toggle-previous"
        :disabled="isPrevButtonDisabled"
      >
        Назад
      </button>
    </li>
    <li class="pagination-item">
      <div class="pages-list">
        <button
          v-for="page in pages"
          @click="onPageClick(page, $event)"
          type="button"
          class="pages-item"
          :class="{'pages-item-current': currentPage === page}"
          :key="page"
        >
          {{ page }}
        </button>
      </div>
    </li>
    <li class="pagination-item">
      <button
        @click="onNextButtonClick"
        class="pagination-toggle pagination-toggle-next"
        :disabled="isNextButtonDisabled"
      >
        Вперед
      </button>
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    pages: {
      type: Number,
      required: true
    },
    currentPage: {
      type: Number,
      required: true
    }
  },

  computed: {
    isPrevButtonDisabled() {
      return this.currentPage === 1;
    },

    isNextButtonDisabled() {
      return this.currentPage === this.pages;
    }
  },

  methods: {
    onPageClick(page, {target}) {
      target.blur();
      this.$emit('update:currentPage', page);
    },

    onPrevButtonClick({target}) {
      target.blur();

      if (this.currentPage !== 1) {
        this.$emit('update:currentPage', this.currentPage - 1);
      }
    },

    onNextButtonClick({target}) {
      target.blur();

      if (this.currentPage < this.pages) {
        this.$emit('update:currentPage', this.currentPage + 1);
      }
    }
  }
}
</script>

<style>
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
}

.pages-item {
  padding: 0;
  border: none;
  color: var(--black-30);
  background-color: inherit;
  cursor: pointer;
}

.pages-item-current {
  pointer-events: none;
  cursor: default;
}

.pages-item:hover,
.pages-item:focus {
  color: var(--black-60);
}

.pages-item-current,
.pages-item-current:hover,
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
  background-color: inherit;
  border: none;
  cursor: pointer;
}

.pagination-toggle:hover,
.pagination-toggle:focus {
  background-color: var(--special-grey-light);
}

.pagination-toggle:active {
  color: var(--black-30);
}

.pagination-toggle:disabled {
  color: var(--black-10);
  background-color: var(--basic-grey-light);
  pointer-events: none;
}
</style>
