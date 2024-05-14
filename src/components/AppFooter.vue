<template>
  <v-footer height="40" app>
    <a v-for="item in items" :key="item.title" :href="item.href" :title="item.title"
      class="d-inline-block mx-2 social-link" rel="noopener noreferrer" target="_blank">
      <v-icon :icon="item.icon" :size="item.icon === '$vuetify' ? 24 : 16" />
    </a>

    <div class="text-caption text-disabled" style="position: absolute; right: 16px;">
      <span class="d-none d-sm-inline-block">This page is for indoor localization display, view</span>
      <a class="text-decoration-none on-surface" href="https://github.com/Dylen-Light" rel="noopener noreferrer"
        target="_blank">
        my git
      </a>
      <span class="d-none d-sm-inline-block"> for more information.</span>
      
    </div>
  </v-footer>
</template>

<script setup>
const items = [
  {
    title: 'This program based on Vuetify',
    icon: `$vuetify`,
    href: 'https://vuetifyjs.com/',
  },
  {
    title: 'my Git',
    icon: `mdi-github`,
    href: 'https://github.com/Dylen-Light',
  },
]
</script>

<style scoped lang="sass">
  .social-link :deep(.v-icon)
    color: rgba(var(--v-theme-on-background), var(--v-disabled-opacity))
    text-decoration: none
    transition: .2s ease-in-out

    &:hover
      color: rgba(25, 118, 210, 1)
</style>
