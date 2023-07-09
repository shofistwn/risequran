<template>
  <div class="bg-gray-100">
    <NuxtLoadingIndicator />

    <Header />

    <main>
      <div class="min-h-screen flex justify-center px-4 sm:px-6 lg:px-0 py-14">
        <div class="max-w-3xl w-full">
          <NuxtPage />
        </div>
      </div>
      <ScrollToTopButton />
    </main>

    <Footer />
  </div>
</template>
