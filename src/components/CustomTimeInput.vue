<template>
    <span class="time-input">
      <input
        type="text"
        v-model="hours"
        @input="validateHours"
        @blur="onBlur"
        maxlength="2"
      />
      <span>:</span>
      <input
        type="text"
        v-model="minutes"
        @input="validateMinutes"
        @blur="onBlur"
        maxlength="2"
      />
    </span>
  </template>
  
  <script>
  export default {
    name: "CustomTimeInput",
    props: {
      value: {
        type: String,
        default: "00:00",
      },
    },
    data() {
      return {
        hours: this.value.split(":")[0],
        minutes: this.value.split(":")[1],
      };
    },
    methods: {
      validateHours() {
        if (!/^\d{0,2}$/.test(this.hours)) {
          this.hours = this.hours.slice(0, -1);
        }
        if (parseInt(this.hours) > 23) {
          this.hours = "23";
        }

        this.emitValue();
      },
      validateMinutes() {
        if (!/^\d{0,2}$/.test(this.minutes)) {
          this.minutes = this.minutes.slice(0, -1);
        }
        if (parseInt(this.minutes) > 59) {
          this.minutes = "59";
        }

        this.emitValue();
      },
      onBlur() {
        this.$emit("blur");
      },
      emitValue() {
        this.$emit("input", `${this.hours.padStart(2, "0")}:${this.minutes.padStart(2, "0")}`);
      },
    },
  };
  </script>
  
  <style scoped>
  .time-input input {
    width: 1.2rem;
    text-align: center;
  }

  </style>