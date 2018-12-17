<template>
  <div class="OpeningHours">
    <div
      v-for="(day, index) in model.days"
      :key="day.name"
      class="OpeningHours__day"
    >
      <h4 class="OpeningHours__day-name">
        {{ day.name }}
      </h4>
      <ol class="OpeningHours__list uk-margin-top-remove uk-margin-bottom-remove">
        <li
          v-for="(time, timeIndex) in day.times"
          :key="timeIndex"
          class="uk-flex uk-flex-middle"
        >
          <input
            v-model="model.days[index].times[timeIndex].start"
            aria-label="Start time"
            class="uk-form-small uk-width-1-1"
            placeholder="09:00 or 9 AM"
          >
          <span class="OpeningHours__separator">
            -
          </span>
          <input
            v-model="model.days[index].times[timeIndex].end"
            aria-label="End time"
            class="uk-form-small uk-width-1-1"
            placeholder="18:00 or 6 PM"
          >
        </li>
      </ol>
    </div>
  </div>
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
        days: [
          {
            name: `Monday`,
            times: [
              {
                start: ``,
                end: ``,
              },
            ],
          },
          {
            name: `Tuesday`,
            times: [
              {
                start: ``,
                end: ``,
              },
            ],
          },
          {
            name: `Wednesday`,
            times: [
              {
                start: ``,
                end: ``,
              },
            ],
          },
          {
            name: `Thursday`,
            times: [
              {
                start: ``,
                end: ``,
              },
            ],
          },
          {
            name: `Friday`,
            times: [
              {
                start: ``,
                end: ``,
              },
            ],
          },
          {
            name: `Saturday`,
            times: [
              {
                start: ``,
                end: ``,
              },
            ],
          },
          {
            name: `Sunday`,
            times: [
              {
                start: ``,
                end: ``,
              },
            ],
          },
        ],
        // This is the name of our plugin.
        plugin: `opening-hours`,
      };
    },
  },
};
</script>

<style>
.OpeningHours__day + .OpeningHours__day {
  margin-top: 10px;
}

.OpeningHours__day-name {
  margin-bottom: 5px;
}

.OpeningHours__list {
  padding-left: 0;
}

.OpeningHours__separator {
  margin-right: 4px;
  margin-left: 4px;
}
</style>
