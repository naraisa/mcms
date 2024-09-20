<!-- <template>
  <div>
    <NuxtRouteAnnouncer />
    <NuxtWelcome />
  </div>
</template> -->
<template>
  <NuxtLayout>
    <header>
      <NuxtLink to="/">header</NuxtLink>
    </header>
    <main>
    <NuxtPage />
    </main>
    <footer>
      footer
    </footer>
  </NuxtLayout>
</template>