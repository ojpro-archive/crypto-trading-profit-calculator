<template>
  <div>
    <input
      type="number"
      class="
        px-2
        py-1.5
        rounded
        border border-gray-700
        bg-gray-800
        focus:shadow
        w-full
      "
      :id="inputName"
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
    />
  </div>
</template>
<script>
export default {
  props: ['modelValue', 'inputName'],
}
</script>