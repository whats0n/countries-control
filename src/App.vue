<template>
  <div :class="$style.page">
    <form :class="$style.countries" @submit.prevent>
      <BaseSearch v-model="search" placeholder="Search" />
      <div :class="$style.filters">
        <BaseSwitcher
          v-model="selectedOnly"
          text="Show selected only"
          :class="$style.filters__switcher"
        />
        <button
          type="button"
          :class="$style.filters__clear"
          @click.prevent="clear"
        >
          Clear all
        </button>
      </div>
      <ul :class="$style.countries__list">
        <template v-if="filteredCountries.length">
          <li
            v-for="country in filteredCountries"
            :key="country"
            :class="$style.countries__item"
          >
            <BaseCheckbox v-model="selected[country]" :text="country" />
          </li>
        </template>
        <li v-else :class="$style.countries__placeholder">
          No Countries was found
        </li>
      </ul>
      <div :class="$style.footer">
        <BaseButton type="submit" text="Save" />
      </div>
    </form>
  </div>
</template>

<script lang="ts" setup>
import { computed, ref, reactive } from 'vue'
import BaseButton from './components/BaseButton.vue'
import BaseCheckbox from './components/BaseCheckbox.vue'
import BaseSearch from './components/BaseSearch.vue'
import BaseSwitcher from './components/BaseSwitcher.vue'

const search = ref<string>('')

const selectedOnly = ref<boolean>(false)

const countries: string[] = [
  'Afghanistan',
  'Algeria',
  'Angola',
  'Andorra',
  'Albania',
  'Argentina',
  'Bahamas',
  'Bangladesh',
  'Belgium',
  'Belarus',
  'Canada',
  'Central African Rep',
  'Congo',
  'Czech Republic',
  'Dominican Republic',
]

const selected = reactive<Record<string, boolean>>(
  countries.reduce<Record<string, boolean>>(
    (result, country) => ({ ...result, [country]: false }),
    {}
  )
)

const filteredCountries = computed<string[]>(() => {
  if (!search.value.length && !selectedOnly.value) return countries

  const query = search.value.toLowerCase()

  return countries.filter(
    (country) =>
      country.toLowerCase().includes(query) &&
      (!selectedOnly.value || selected[country])
  )
})

const clear = (): void => {
  countries.forEach((key) => {
    selected[key] = false
  })
}
</script>

<style lang="scss" module>
.page {
  padding: 20px;
}

.countries {
  margin-inline: auto;
  padding: 20px;
  border: 1px solid #e1e3e6;
  border-radius: 14px;
  max-width: 494px;
  background: #ffffff;
  box-shadow: 9px 32px 35px rgba(0, 0, 0, 0.0464653);

  &__list {
    display: flex;
    flex-direction: column;
    overflow: auto;
    padding-bottom: 15px;
    height: 247px;
  }

  &__item:not(:last-child) {
    margin-bottom: 20px;
  }

  &__placeholder {
    margin: auto;
    font-weight: 500;
    font-size: 16px;
    line-height: 22px;
    text-align: center;
  }
}

.filters {
  display: flex;
  flex-wrap: wrap;
  padding-block: 15px;

  > * {
    margin: 8px 0;
  }

  &__switcher {
    margin-right: auto;
    padding-right: 10px;
  }

  &__clear {
    flex: 0 0 auto;
    height: 22px;
    color: #232323;
    font-weight: 500;
    font-size: 16px;
    line-height: normal;
    letter-spacing: -0.5px;
    transition: color 0.3s;

    &:hover,
    &:focus-visible {
      color: #60d09b;
    }
  }
}

.footer {
  position: relative;
  display: flex;
  justify-content: flex-end;
  padding-top: 20px;

  &:before {
    content: '';
    position: absolute;
    inset: 0 0 auto;
    display: block;
    border-radius: 1px;
    height: 1px;
    background: #ececec;
  }
}
</style>
