<template>
  <label :class="$style.switcher">
    <input v-model="value" type="checkbox" />
    <span :class="$style.switcher__figure" />
    <span :class="$style.switcher__text">
      {{ text }}
    </span>
  </label>
</template>

<script lang="ts" setup>
import { computed } from 'vue'

const props = defineProps<{
  modelValue: boolean
  text: string
}>()

const emit = defineEmits<{
  (e: 'update:modelValue', value: boolean): void
}>()

const value = computed<boolean>({
  get: () => props.modelValue,
  set: (value) => emit('update:modelValue', value),
})
</script>

<style lang="scss" module>
.switcher {
  position: relative;
  display: flex;
  align-items: flex-start;
  cursor: pointer;
  user-select: none;

  &__figure {
    position: relative;
    display: block;
    flex: 0 0 auto;
    margin-right: 10px;
    border-radius: 11px;
    width: 37px;
    height: 22px;
    background: rgba(0, 28, 61, 0.08);
    transition: background-color 0.3s;

    &:before {
      content: '';
      position: absolute;
      inset: 1px auto 1px 1px;
      border-radius: 50%;
      aspect-ratio: 1/1;
      background: #ffffff;
      box-shadow: 0px 2.17647px 5.80392px rgba(0, 0, 0, 0.15);
      transition: transform 0.3s;
    }
  }

  &__text {
    flex: 1 1 auto;
    color: #232323;
    font-weight: 500;
    font-size: 16px;
    line-height: 22px;
    letter-spacing: -0.5px;
    transition: color 0.3s;
  }

  input {
    position: absolute;
    top: 0;
    left: 0;
    opacity: 0;
  }

  input:checked ~ .switcher__figure {
    background-color: #60d09b;

    &:before {
      transform: translateX(15px);
    }
  }

  input:focus-visible ~ .switcher__text,
  &:hover input ~ .switcher__text {
    color: #60d09b;
  }
}
</style>
