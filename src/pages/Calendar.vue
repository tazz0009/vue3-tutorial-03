<template>
  <div class="m-auto">
    <h1 class="text-center text-3xl my-4">
      Vue Calendar
    </h1>
    <section class="mx-2 flex justify-between">
      <h2 class="font-bold">{{ cuurentYear }}년</h2>
      <h2 class="font-bold">
        {{ currentMonthName }}
      </h2>
    </section>
    <section class="flex my-2">
      <p
        class="text-center"
        style="width: 14.28%"
        v-for="day in days"
        :key="day"
      >
        {{ day }}
      </p>
    </section>
    <section class="flex flex-wrap">
      <p
        class="text-center"
        style="width: 14.28%"
        v-for="num in startDay()"
        :key="num"
      ></p>
      <p
        class="text-center"
        style="width: 14.28%"
        v-for="num in daysInMonth()"
        :key="num"
        :class="currentDateClass(num)"
      >
        {{ num }}
      </p>
    </section>
    <section class="flex justify-between my-4">
      <button class="px-2 border rounded" @click="prev">Prev</button>
      <button class="px-2 border rounded" @click="next">Next</button>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentDate: new Date().getUTCDate(),
      currentMonth: new Date().getMonth(),
      cuurentYear: new Date().getFullYear(),
      days: ["Sun", "Mon", "Tue", "Wed", "Tur", "Fri", "Sat"],
    };
  },
  methods: {
    daysInMonth() {
      return new Date(this.cuurentYear, this.currentMonth + 1, 0).getDate();
    },
    startDay() {
      return new Date(this.cuurentYear, this.currentMonth, 1).getDay();
    },
    next() {
      if (this.currentMonth === 11) {
        this.currentMonth = 0;
        this.cuurentYear++;
      } else {
        this.currentMonth++;
      }
    },
    prev() {
      if (this.currentMonth === 0) {
        this.currentMonth = 11;
        this.cuurentYear--;
      } else {
        this.currentMonth--;
      }
    },
    currentDateClass(num) {
      const calendarFullDate = new Date(
        this.cuurentYear,
        this.currentMonth,
        num
      ).toDateString();
      const currentFullDate = new Date().toDateString();
      return calendarFullDate === currentFullDate ? "text-yellow-600" : "";
    },
  },
  computed: {
    currentMonthName() {
      return new Date(
        this.cuurentYear,
        this.currentMonth
      ).toLocaleString("default", { month: "long" });
    },
  },
};
</script>

<style></style>
