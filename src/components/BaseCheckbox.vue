<template>
  <label :class="$style.checkbox">
    <input v-model="value" type="checkbox" />
    <span :class="$style.checkbox__figure">
      <svg viewBox="0 0 14 11" :class="$style.checkbox__icon">
        <path
          d="M13.5656 2.38749L6.19322 9.75932C5.64729 10.3054 4.76171 10.3054 4.21526 9.75932L0.409603 5.95339C-0.136534 5.40735 -0.136534 4.52166 0.409603 3.97553C0.955845 3.42928 1.84136 3.42928 2.38736 3.97532L5.20453 6.79253L11.5875 0.409526C12.1337 -0.136716 13.0193 -0.136302 13.5654 0.409526C14.1114 0.955664 14.1114 1.84104 13.5656 2.38749Z"
        />
      </svg>
    </span>
    <span :class="$style.checkbox__text">
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
.checkbox {
  position: relative;
  display: flex;
  align-items: flex-start;
  color: #343434;
  cursor: pointer;
  user-select: none;

  &__figure {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    flex: 0 0 auto;
    margin-right: 15px;
    border-radius: 8px;
    width: 22px;
    height: 22px;
    background: #ececec;
    transition: background-color 0.3s;
  }

  &__icon {
    width: 14px;
    height: 11px;
    fill: #c4c4c4;
    opacity: 0;
    transition: fill 0.3s, opacity 0.3s;
  }

  &__text {
    flex: 1 1 auto;
    align-self: center;
    font-weight: 500;
    font-size: 16px;
    line-height: 1;
    letter-spacing: -0.5px;
  }

  input {
    position: absolute;
    top: 0;
    left: 0;
    opacity: 0;
  }

  input:checked ~ .checkbox {
    &__figure {
      background-color: #457df1;

      .checkbox__icon {
        fill: #fff;
        opacity: 1;
      }
    }
  }

  input:not(:checked):focus-visible ~ .checkbox {
    &__figure {
      background: #ececec;

      .checkbox__icon {
        opacity: 1;
      }
    }
  }

  &:hover {
    input:not(:checked) ~ .checkbox {
      &__figure {
        background: #ececec;

        .checkbox__icon {
          opacity: 1;
        }
      }
    }
  }
}
</style>
