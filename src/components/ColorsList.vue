<template>
  <ul class="colors">
    <li class="colors__item" v-for="color in colors" :key="color.id">
      <label class="colors__label">
        <input class="colors__radio sr-only" type="radio" :name="elementName" :value="color.id" v-model="currentColorComponent" >
        <span class="colors__value" :style="'background-color:' + color.code">
        </span>
      </label>
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    colors: Array,
    currentColor: Number,
    elementName: String,
  },
  computed: {
    currentColorComponent: {
      get() {
        return this.currentColor;
      },
      set(value) {
        this.$emit('update:currentColor', value);
      },
    },
  },
};
</script>