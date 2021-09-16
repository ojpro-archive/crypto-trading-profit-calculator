<template>
  <button
    class="
      bg-blue-500
      text-white
      rounded
      focus:shadow-sm
      focus:bg-blue-400
      px-2
      py-1.5
      w-full
      mt-3
    "
  >
    {{ name }}
  </button>
</template>
<script>
export default {
    props:['name']
}
</script>