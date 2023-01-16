<template>
  <ul class="pagination">
    <li class="pagination-item">
      <a class="pagination-toggle pagination-toggle-previous" href="#">Назад</a>
    </li>
    <li class="pagination-item">
      <ul class="pages-list">
        <li v-for="page in pages" class="pages-item">
          <a href="#">{{ page }}</a>
        </li>
      </ul>
    </li>
    <li class="pagination-item">
      <a class="pagination-toggle pagination-toggle-next" href="#">Вперед</a>
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    pages: {
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