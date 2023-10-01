<template>
  <main class="content container">
    <div class="content__top">
      <ul class="breadcrumbs">
        <li class="breadcrumbs__item">
          <a class="breadcrumbs__link" href="index.html">
            Каталог
          </a>
        </li>
        <li class="breadcrumbs__item">
          <a class="breadcrumbs__link" href="cart.html">
            Корзина
          </a>
        </li>
        <li class="breadcrumbs__item">
          <a class="breadcrumbs__link">
            Оформление заказа
          </a>
        </li>
      </ul>

      <h1 class="content__title">
        Заказ оформлен <span>№ 23621</span>
      </h1>
    </div>

    <section class="cart">
      <form class="cart__form form" action="#" method="POST">
        <div class="cart__field">
          <p class="cart__message">
            Благодарим за&nbsp;выбор нашего магазина. На&nbsp;Вашу почту придет письмо с&nbsp;деталями заказа.
            Наши менеджеры свяжутся с&nbsp;Вами в&nbsp;течение часа для уточнения деталей доставки.
          </p>
          <!-- Информация о заказе -->
          <ul class="dictionary">
            <li class="dictionary__item">
              <span class="dictionary__key">
                Получатель
              </span>
              <span class="dictionary__value" v-if="orderInfo">
                {{ orderInfo.name }}
              </span>
            </li>
            <li class="dictionary__item">
              <span class="dictionary__key">
                Адрес доставки
              </span>
              <span class="dictionary__value" v-if="orderInfo">
                 {{ orderInfo.address }}
              </span>
            </li>
            <li class="dictionary__item">
              <span class="dictionary__key">
                Телефон
              </span>
              <span class="dictionary__value" v-if="orderInfo">
                {{ orderInfo.phone }}
              </span>
            </li>
            <li class="dictionary__item">
              <span class="dictionary__key">
                Email
              </span>
              <span class="dictionary__value" v-if="orderInfo">
                {{ orderInfo.email }}
              </span>
            </li>
            <li class="dictionary__item">
              <span class="dictionary__key">
                Способ оплаты
              </span>
              <span class="dictionary__value">
                картой при получении
              </span>
            </li>
          </ul>
        </div>
        <!-- Список товаров -->
        <div class="cart__block">
          <ul class="cart__orders">
            <OrderList  v-for="item in orderProducts" :key="item.productId" :item="item" />
          </ul>
          <div class="cart__total" v-if="orderInfo">
            <p>Доставка: <b>Бесплатно ₽</b></p>
            <p>Итого товаров: <b>{{ orderInfo.totalAmount }}</b> на сумму <b>{{ orderInfo.totalPrice | numberFormat }} ₽</b></p>
          </div>
        </div>
      </form>
    </section>
  </main>
</template>
<script>
  import OrderList from "@/components/OrderList.vue";
  import {mapGetters} from "vuex";
  import numberFormat from "@/helpers/numberFormat";
  export default {
    filters: { numberFormat },
    components: { OrderList },
    computed: {
      ...mapGetters({ orderProducts: 'orderProducts' }),
      orderInfo() {
        return this.$store.state.orderInfo;
      },
    },
    created() {
      if (
          this.$store.state.orderInfo && this.$store.state.orderInfo.id === this.$route.params.id
      ) {
        return;
      }

      this.$store.dispatch('loadOrderInfo', this.$route.params.id);
    },
  };
</script>
