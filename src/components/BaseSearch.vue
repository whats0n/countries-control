<template>
  <div :class="$style.search">
    <input
      v-model="value"
      type="text"
      :placeholder="placeholder"
      :class="$style.search__input"
    />
  </div>
</template>

<script lang="ts" setup>
import { computed } from 'vue'

const props = defineProps<{
  modelValue: string
  placeholder: string
}>()

const emit = defineEmits<{
  (e: 'update:modelValue', value: string): void
}>()

const value = computed<string>({
  get: () => props.modelValue,
  set: (value) => emit('update:modelValue', value),
})
</script>

<style lang="scss" module>
.search {
  position: relative;

  &:after {
    content: '';
    position: absolute;
    inset: auto 0 0;
    display: block;
    border-radius: 1px;
    height: 1px;
    background: #ececec;
  }

  &__input {
    display: block;
    width: 100%;
    height: 32px;
    padding-bottom: 12px;
    color: #343434;
    font-size: 16px;
    line-height: normal;
    letter-spacing: -0.5px;

    &::placeholder {
      opacity: 1;
      color: inherit;
    }
  }
}
</style>
