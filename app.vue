<template>
  <div>
    <h3>Available locales:</h3>

    <pre>{{ availableLocales }}</pre>

    <hr />

    <h3>Switch language:</h3>

    <nuxt-link
      v-for="locale in availableLocales"
      :key="locale.code"
      :to="switchLocalePath(locale.code)"
    >
      {{ locale.name }}
    </nuxt-link>

    <hr />

    <h1>{{ $t('hello') }}</h1>
  </div>
</template>

<script lang="ts" setup>
const i18n = useI18n();
const switchLocalePath = useSwitchLocalePath();

const availableLocales = computed(() => i18n.locales.value);

const currentLocale = computed(() =>
  availableLocales.value.find(({ code }) => code === i18n.locale.value)
);

const isMounted = ref(false);
onMounted(() => {
  isMounted.value = true;

  setTimeout(() => i18n.setLocale('fr'), 5000);
});
</script>

<style lang="css" scoped>
a,
img {
  margin: 0 10px;
}
</style>
