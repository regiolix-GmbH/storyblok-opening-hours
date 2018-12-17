<template>
  <div class="OpeningHours"/>
</template>

<script>
export default {
  mixins: [window.Storyblok.plugin],
  watch: {
    model: {
      deep: true,
      handler(value) {
        // Let Storyblok know that the value was updated.
        this.$emit(`changed-model`, value);
      },
    },
  },
  methods: {
    initWith() {
      return {
        // This array will be filled with the opening
        // hours for every specific day of the week.
        days: [],
        // This is the name of our plugin.
        plugin: `opening-hours`,
      };
    },
  },
};
</script>
