<template>
  <li class="catalog__item">
            <router-link class="catalog__pic" href="#" :to="{name: 'product', params: {id: product.id}}">
              <img :src="product.image" :alt="product.title">
            </router-link>

            <h3 class="catalog__title">
              <a href="#">
                {{ product.title }}
              </a>
            </h3>

            <span class="catalog__price">
              {{ product.price | numberFormat }}
            </span>

    <ColorsList class="colors--black" :colors="colors" :elementName="'product_' + product.id" :current-color="firstColor"/>
  </li>
</template>

<script>
import gotoPage from "@/helpers/gotoPage";
import numberFormat from "@/helpers/numberFormat";
import ColorsList from "@/components/ColorsList.vue";
export default {
  components: {ColorsList},
  data() {
    return {
      color: '#000'
    }
  },
  filters: {
    numberFormat
  },
  computed: {
    colors() {
      return this.product.colors;
    },
    firstColor() {
      return this.colors[0].id;
    },
  },
  methods: {
    gotoPage
  },
  props: ['product']
}
</script>
