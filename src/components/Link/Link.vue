<template>
  <div>
    <a :href="link" target="_blank">
      <div class="w-16 h-16 relative box flex items-center justify-center outline-none">
        <div class="w-2 h-2 corner absolute opacity-30 left-0 top-0 border-t border-l"></div>
        <div class="w-2 h-2 corner absolute opacity-30 right-0 top-0 border-t border-r"></div>
        <div class="w-2 h-2 corner absolute opacity-30 right-0 bottom-0 border-r border-b"></div>
        <div class="w-2 h-2 corner absolute opacity-30 left-0 bottom-0 border-l border-b"></div>
        <p class="prata text-white">{{ content }}</p>
      </div>
    </a>
  </div>

</template>

<script>
export default {
  name: 'Link',
  props: ['content', 'link']
}
</script>

<style lang="scss" scoped>
.corner{
  transition: all linear .1s;
}
.box:hover .corner{
  width: 2rem;
  height: 2rem;
}
</style>
