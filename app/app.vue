<script setup>
const { loggedIn } = useUserSession()
const colorMode = useColorMode()

watch(loggedIn, () => {
  if (!loggedIn.value) {
    navigateTo('/')
  }
})

function toggleColorMode() {
  colorMode.preference = colorMode.preference === 'dark' ? 'light' : 'dark'
}

useHead({
  htmlAttrs: { lang: 'en' },
  link: [{ rel: 'icon', href: '/icon.png' }]
})

useSeoMeta({
  viewport: 'width=device-width, initial-scale=1, maximum-scale=1',
  title: 'Todo with Passkeys',
  description:
    'A Nuxt demo hosted on NuxtHub using passkeys for authentication and queyring a Cloudflare D1 database',
  ogImage: '/social-image.png',
  twitterImage: '/social-image.png',
  twitterCard: 'summary_large_image'
})
</script>

<template>
  <UContainer class="min-h-screen flex flex-col justify-center">
    <div class="mb-2 text-right">
      <UButton
        square
        variant="ghost"
        color="black"
        :icon="$colorMode.preference === 'dark' ? 'i-heroicons-moon' : 'i-heroicons-sun'"
        @click="toggleColorMode"
      />
    </div>

    <NuxtPage />

    <footer class="text-center mt-2">
      <NuxtLink
        href="https://github.com/atinux/todo-passkeys"
        target="_blank"
        class="text-sm text-gray-500 hover:text-gray-700"
      >
        source code
      </NuxtLink>
      ·
      <NuxtLink
        href="https://twitter.com/atinux"
        target="_blank"
        class="text-sm text-gray-500 hover:text-gray-700"
      >
        @atinux
      </NuxtLink>
    </footer>
  </UContainer>
  <UNotifications />
</template>

<style lang="postcss">
body {
  @apply font-sans text-gray-950 bg-gray-50 dark:bg-gray-950 dark:text-gray-50;
}
</style>
