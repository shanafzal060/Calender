<template>
  <div class="container" >
    <div class="row">


      <div class="col-lg-6 bg-primary center">
        <div>
          <h1>Today's Date is</h1>
          <h1 class="display-1">{{ showDate }}</h1>
        </div>
      </div>


      <div class="col-lg-6">
        <section>
          <h1>My VUE Calender</h1>
        </section>
        <section>
          <h1>{{ currentMonthName }} {{ currentYear }}</h1>
        </section>
        <section class="days d-flex">
          <p class="text-center" v-for="day in days" :key="day">{{ day }}</p>
        </section>
        <section>
          <div class="dates d-flex">
            <p class="text-center" v-for="day in firstDay" :key="day"></p>
            <p
              :class="todayDate(date)"
              class="text-center"
              v-for="date in lastDateOfMonth"
              :key="date"
            >
              {{ date }}
            </p>
          </div>
        </section>
        <section class="d-flex justify-content-between">
          <button class="btn btn-primary" tabindex="0" @keydown.left="prev" @click="prev">Prev</button>
          <button class="btn btn-primary" tabindex="0" @keydown.right="next" @click="next">Next</button>
        </section>
      </div>
    </div>
  </div>
</template>

<script>

import { ref, computed } from "vue";

export default {

  name: "VueCalender",

  setup() {
    const days = ref(["MON", "TUE", "WED", "THU", "FRI", "SAT", "SUN"]);
    const currentMonthInNumber = ref(new Date().getMonth());
    const currentYear = ref(new Date().getFullYear());
    const showDate = ref(new Date().getDate());

    const currentMonthName = computed(() => {
      return new Date(
        currentYear.value,
        currentMonthInNumber.value
      ).toLocaleString("default", { month: "long" });
    });

    const lastDateOfMonth = computed(() => {
      return new Date(
        currentYear.value,
        currentMonthInNumber.value + 1,
        0
      ).getDate();
    });
    const firstDay = computed(() => {
      return new Date(
        currentYear.value,
        currentMonthInNumber.value,
        1
      ).getDay();
    });

    const todayDate = (date) => {
      let calenderDate = new Date(
        currentYear.value,
        currentMonthInNumber.value,
        date
      ).toDateString();
      let today = new Date().toDateString();
      return calenderDate === today ? "btn btn-primary btn-sm text-light " : "";
    };

    const prev = () => {
      if (currentMonthInNumber.value === 0) {
        currentYear.value--;
        currentMonthInNumber.value = 11;
      } else {
        currentMonthInNumber.value--;
      }
      console.log(currentMonthInNumber.value);
    };

    const next = () => {
      if (currentMonthInNumber.value === 11) {
        currentYear.value++;
        currentMonthInNumber.value = 0;
      } else {
        currentMonthInNumber.value++;
      }
      console.log(currentMonthInNumber.value);
    };

    return {
      days,
      currentMonthInNumber,
      currentMonthName,
      currentYear,
      todayDate,
      lastDateOfMonth,
      firstDay,
      prev,
      next,
      showDate,
    };
  },
};
</script>

<style>
.days p,
.dates p {
  width: 14.28%;
}
.dates {
  flex-wrap: wrap;
}
.center{
  display: flex;
  justify-content: center;
  align-items: center;
  color: aliceblue;
}
</style>
