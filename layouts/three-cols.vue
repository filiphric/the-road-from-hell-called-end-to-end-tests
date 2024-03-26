<!-- default.vue -->
<template class="two-columns">
  <div class="grid grid-cols-3 place-items-center py-10 gap-4">
    <div class="justify-self-center">
      <slot name="left" />
    </div>
    <div class="justify-self-center">
      <slot name="center" />
    </div>
    <div class="justify-self-center">
      <slot name="right" />
    </div>
  </div>
</template>
<style>
#slideshow {
  background-color: var(--slidev-theme-background);
}
</style>