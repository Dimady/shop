<template>
  <li class="cart__order">
    <h3>{{ item.product.title }}</h3>
    <b>{{ item.costAmount | numberFormat }} ₽</b>
    <span>Артикул: {{ item.product.id }}</span>
    <span>Количество: {{ item.amount }}</span>
  </li>
</template>

<script>
import numberFormat from '@/helpers/numberFormat';

export default {
  filters: { numberFormat },
  props: ['item'],
};
</script>