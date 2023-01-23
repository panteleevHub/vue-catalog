<template>
  <ul class="pagination">
    <li class="pagination-item">
      <button class="pagination-toggle pagination-toggle-previous">Назад</button>
    </li>
    <li class="pagination-item">
      <div class="pages-list">
        <button
          v-for="page in pages"
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
      <button class="pagination-toggle pagination-toggle-next">Вперед</button>
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
}

.pagination-toggle:hover,
.pagination-toggle:focus {
  background-color: var(--special-grey-light);
}

.pagination-toggle:active {
  color: var(--black-30);
}
</style>
