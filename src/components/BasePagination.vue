<template>
  <ul class="catalog__pagination pagination">
    <li class="pagination__item">
      <a class="pagination__link pagination__link--arrow"
         href="#" aria-label="Предыдущая страница" @click.prevent="previous(page)">
        <svg width="8" height="14" fill="currentColor">
          <use xlink:href="#icon-arrow-left"></use>
        </svg>
      </a>
    </li>
    <li class="pagination__item" v-for="pageNumber in pages" :key="pageNumber">
      <a href="#" class="pagination__link" :class="{'pagination__link--current': pageNumber === page}"
         @click.prevent="paginate(pageNumber)">
        {{ pageNumber }}
      </a>
    </li>
    <li class="pagination__item">
      <a class="pagination__link pagination__link--arrow" href="#" aria-label="Следующая страница"
         @click.prevent="next(page)">
      <svg width="8" height="14" fill="currentColor">
          <use xlink:href="#icon-arrow-right"></use>
        </svg>
      </a>
    </li>
  </ul>
</template>
<script>
  export default {
    model: {
      prop: 'page',
      event: 'paginate'
    },
    props: ['page', 'count', 'perPage'],
    computed: {
      pages() {
        return Math.ceil(this.count / this.perPage);
      }
    },
    methods: {
      paginate(page) {
        this.$emit('paginate', page);
      },
      next(page) {
        if (page === this.pages) {
          this.paginate(page);
        } else {
          this.paginate(page + 1);
        }
      },
      previous(page) {
        if (page === 1) {
          this.paginate(page);
        } else {
          this.paginate(page - 1);
        }
      }
    }
  }
</script>