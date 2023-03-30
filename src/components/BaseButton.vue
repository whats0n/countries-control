<template>
  <button :type="type" :class="$style.button">
    {{ text }}
  </button>
</template>

<script lang="ts" setup>
withDefaults(
  defineProps<{
    type?: 'button' | 'submit'
    text: string
  }>(),
  { type: 'button' }
)
</script>

<style lang="scss" module>
.button {
  display: inline-block;
  vertical-align: top;
  padding-inline: 25px;
  border-radius: 19px;
  height: 38px;
  color: #fff;
  background: #60d09b;
  font-weight: 400;
  font-size: 16px;
  line-height: normal;
  letter-spacing: -0.5px;
  transition: opacity 0.3s;

  &:hover,
  &:focus-visible {
    opacity: 0.7;
  }
}
</style>
