<template>
  <li class="catalog__item">
            <a class="catalog__pic" href="#" @click.prevent="gotoPage('product', {id: product.id})">
              <img :src="product.image" :alt="product.title">
            </a>

            <h3 class="catalog__title">
              <a href="#">
                {{ product.title }}
              </a>
            </h3>

            <span class="catalog__price">
              {{ product.price | numberFormat }}
            </span>

            <ul class="colors colors--black">
              <li class="colors__item">
                <label class="colors__label">
                  <input class="colors__radio sr-only" type="radio" value="#000" v-model="color">
                  <span class="colors__value" style="background-color: #000;">
                  </span>
                </label>
              </li>
              <li class="colors__item">
                <label class="colors__label">
                  <input class="colors__radio sr-only" type="radio" value="#FFBE15" v-model="color">
                  <span class="colors__value" style="background-color: #FFBE15;">
                  </span>
                </label>
              </li>
              <li class="colors__item">
                <label class="colors__label">
                  <input class="colors__radio sr-only" type="radio" value="#939393" v-model="color">
                  <span class="colors__value" style="background-color: #939393;">
                  </span>
                </label>
              </li>
            </ul>
  </li>
</template>

<script>
import gotoPage from "@/helpers/gotoPage";
import numberFormat from "@/helpers/numberFormat";
export default {
  data() {
    return {
      color: '#000'
    }
  },
  filters: {
    numberFormat
  },
  methods: {
    gotoPage
  },
  props: ['product']
}
</script>
