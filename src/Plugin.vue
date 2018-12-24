<template>
  <div class="OpeningHours">
    <div
      v-for="(day, index) in model.days"
      :key="day.name"
      class="OpeningHours__day"
    >
      <h4 class="OpeningHours__day-name">
        {{ day.name }}
        <a
          v-if="index !== 0"
          aria-label="Copy from previous day"
          @click="copyFromPreviousDay(index)"
        >
          <i class="uk-icon-copy"/>
        </a>
      </h4>
      <ol class="OpeningHours__list uk-margin-top-remove uk-margin-bottom-remove">
        <li
          v-for="(time, timeIndex) in day.times"
          :key="timeIndex"
          class="OpeningHours__list-item uk-flex uk-flex-middle"
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
          <a
            class="assets__item-trash"
            aria-label="Remove item"
            @click="removeFields(index, timeIndex)"
          >
            <i class="uk-icon-minus-circle"/>
          </a>
        </li>
      </ol>
      <a
        class="blok__full-btn uk-margin-small-top"
        @click="addFields(index)"
      >
        <i class="uk-icon-plus-circle uk-margin-small-right"/>
        Add fields
      </a>
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
    addFields(index) {
      this.model.days[index].times.push({
        start: ``,
        end: ``,
      });
    },
    removeFields(dayIndex, timeIndex) {
      this.model.days[dayIndex].times = this.model.days[dayIndex].times
        .filter((_, i) => i !== timeIndex);
    },
    copyFromPreviousDay(index) {
      this.model.days[index].times = this.model.days[index - 1].times
        .map(x => ({ start: x.start, end: x.end }));
    },
    initWith() {
      return {
        days: [
          {
            name: `Monday`,
            times: [],
          },
          {
            name: `Tuesday`,
            times: [],
          },
          {
            name: `Wednesday`,
            times: [],
          },
          {
            name: `Thursday`,
            times: [],
          },
          {
            name: `Friday`,
            times: [],
          },
          {
            name: `Saturday`,
            times: [],
          },
          {
            name: `Sunday`,
            times: [],
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
  display: flex;
  margin-bottom: 5px;
  justify-content: space-between;
}

.OpeningHours__list {
  padding-left: 0;
}

.OpeningHours__list-item + .OpeningHours__list-item {
  margin-top: 5px;
}

.OpeningHours__separator {
  margin-right: 4px;
  margin-left: 4px;
}
</style>
