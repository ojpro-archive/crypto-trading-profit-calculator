<template>
  <div class="p-2">
    <div class="text-center mt-4">
      <span>
        Created with 💖 by <a href="https://github.com/ojpro" class="text-blue-300 hover:text-purple-400">ojpro</a>(Oussama ELJabbari) - {{ currentYear() }}
      </span>
    </div>
  </div>
</template>
<script>
export default {
  methods: {
    currentYear: function () {
      let date = new Date()
      return date.getFullYear()
    },
  },
}
</script>