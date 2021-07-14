<template>
  <header class="page-header">
    <nav id="nav">
      <router-link to="/">{{ $t('home') }}</router-link>
      |
      <router-link to="/about">{{ $t('about') }}</router-link>
    </nav>
    <ul class="page-header__lang-list">
      <li
        class="page-header__lang-item"
        v-for="lang in languages"
        :key="lang"
        @click="onChangeLang(lang)"
      >
        {{ lang.toUpperCase() }}
      </li>
    </ul>
  </header>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import i18n from '@/plugins/vue-i18n';

export default defineComponent({
  name: 'PageHeader',
  setup() {
    const languages = Object.keys(i18n.global.messages);

    const onChangeLang = (target: string): void => {
      i18n.global.locale = target.toLowerCase();
    };

    return {
      languages,
      onChangeLang,
      i18n,
    };
  },
});
</script>

<style scoped lang="scss">
.page-header {
  &__lang-list {
    display: flex;
    justify-content: center;
    padding: 0;
    list-style: none;
  }

  &__lang-item {
    color: $color-text;
    font-weight: 700;
    font-size: 18px;
    cursor: pointer;

    &:hover {
      color: $color-link;
    }

    &:not(:last-child) {
      margin-right: 10px;
    }
  }
}
</style>
