<template>
  <div class="date-picker">
    <div class="date-picker-header">
      <button class="prev-btn" @click.prevent="moveMonth('backward')">prev</button>
      <h2>{{ currentMonth + 1 }}月 {{ currentYear }}年</h2>
      <button class="next-btn" @click.prevent="moveMonth('forward')">next</button>
    </div>
    <div class="seven-days">
      <ul>
        <li>日</li>
        <li>一</li>
        <li>二</li>
        <li>三</li>
        <li>四</li>
        <li>五</li>
        <li>六</li>
      </ul>
    </div>
    <div class="months-wrapper" ref="monthsWrapper">
      <div class="month-mover" ref="monthMover">
        <ul class="month" ref="prevMonth">
          <li v-for="day in months[prevMonth].days" :key="day" class="day">{{ day }}</li>
        </ul>
        <ul class="month" ref="currentMonth">
          <li
            v-for="day in months[currentMonth].days"
            :key="day"
            class="day"
            @click="$emit('setDate', `${currentMonth}/${day}/${currentYear}`)"
          >{{ day }}</li>
        </ul>
        <ul class="month" ref="nextMonth">
          <li v-for="day in months[nextMonth].days" :key="day" class="day">{{ day }}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "DatePicker",
  props: {
    secondDate: String
  },
  watch: {
    prevMonth(newVal) {
      if (newVal < 0) {
        this.prevMonth = 11;
      }
      if (newVal > 11) {
        this.prevMonth = 0;
      }
    },
    nextMonth(newVal) {
      if (newVal < 0) {
        this.nextMonth = 11;
      }
      if (newVal > 11) {
        this.nextMonth = 0;
      }
    },
    currentMonth(newVal) {
      if (newVal < 0) {
        this.currentMonth = 11;
        this.currentYear -= 1;
      }
      if (newVal > 11) {
        this.currentMonth = 0;
        this.currentYear += 1;
      }
    }
  },
  data() {
    const now = new Date();
    return {
      currentYear: now.getFullYear(),
      currentMonth: now.getMonth(),
      prevMonth: now.getMonth() - 1,
      nextMonth: now.getMonth() + 1,
      preselectedDate: this.seondDate || now.getDate(),
      months: [
        { name: "January", days: this.getDays(0) },
        { name: "February", days: this.getDays(1) },
        { name: "March", days: this.getDays(2) },
        { name: "April", days: this.getDays(3) },
        { name: "May", days: this.getDays(4) },
        { name: "June", days: this.getDays(5) },
        { name: "July", days: this.getDays(6) },
        { name: "August", days: this.getDays(7) },
        { name: "September", days: this.getDays(8) },
        { name: "October", days: this.getDays(9) },
        { name: "November", days: this.getDays(10) },
        { name: "December", days: this.getDays(11) }
      ]
    };
  },
  methods: {
    // get number of days of that month in currentYear(for February)
    getDays(month, year = new Date().getFullYear()) {
      return new Date(year, month + 1, 0).getDate();
    },
    setMonthWidth() {
      const { monthsWrapper, month } = this.$refs;
      monthUl.forEach(ml => {
        ml.style.width = monthsWrapper.clientWidth + "px";
      });
    },
    setDayHeights(month) {
      const days = this.$refs[month].children;
      const daysArr = Array.from(days);
      const dayWidth = daysArr[0].getBoundingClientRect().width;

      daysArr.forEach(day => (day.style.height = `${dayWidth}px`));
    },
    moveToCurrentMonth() {
      const { monthMover, currentMonth } = this.$refs;

      monthMover.style.transform = `translateX(-${currentMonth.clientWidth}px)`;
    },
    setFirstDayPosition(month, year = this.currentYear) {
      const m = this.$refs[month];
      // get the first day of the month
      const weekday = new Date(year, this[month], 1).getDay();

      // set the margin left of the first li in month
      m.firstChild.style.marginLeft = `
        ${m.firstChild.getBoundingClientRect().width * weekday}px
      `;
    },
    setMonthHeight(month) {},
    // move forward and backwoard
    moveMonth(direction) {
      const { monthMover, currentMonth, nextMonth, prevMonth } = this.$refs;

      // transitionend callback
      const transitionendCallback = e => {
        if (e.propertyName === "transform") {
          // change current month
          direction === "forward" ? this.currentMonth++ : this.currentMonth--;

          this.$nextTick(() => {
            this.setDayHeights("currentMonth");
            this.setFirstDayPosition("currentMonth");

            // move back to original position
            monthMover.style.transition = "transform 0s linear";
            monthMover.style.transform = `
          translateX(-${currentMonth.clientWidth}px)
        `;

            monthMover.removeEventListener(
              "transitionend",
              transitionendCallback
            );

            if (direction === "forward") {
              this.nextMonth++;
              this.prevMonth++;
            } else if (direction === "backward") {
              this.nextMonth--;
              this.prevMonth--;
            }
          });
        }
      };

      // after sliding animation completed
      monthMover.addEventListener("transitionend", transitionendCallback);

      if (direction === "forward") {
        this.setFirstDayPosition(
          "nextMonth",
          this.nextMonth == 0 ? this.currentYear + 1 : this.currentYear
        );
        this.setDayHeights("nextMonth");

        // sliding animation
        monthMover.style.transition = "transform .2s linear";
        monthMover.style.transform = `
          translateX(-${currentMonth.clientWidth * 2 + 40}px)
        `;
      } else if (direction === "backward") {
        this.setFirstDayPosition(
          "prevMonth",
          this.prevMonth == 0 ? this.currentYear - 1 : this.currentYear
        );
        this.setDayHeights("prevMonth");
        // sliding animation
        monthMover.style.transition = "transform .2s linear";
        monthMover.style.transform = `translateX(40px)`;
      }
    },
    apply(day) {
      console.log(`${this.currentMonth + 1} / ${day} / ${this.currentYear}`);
    }
  },
  mounted() {
    // this.setMonthWidth();
    this.moveToCurrentMonth();
    this.setFirstDayPosition("currentMonth");
    this.setDayHeights("currentMonth");
    this.setMonthHeight("currentMonth");
  }
};
</script>

<style lang="scss" scoped>
.date-picker {
  position: relative;
  width: 300px;
  padding: 20px;
  box-shadow: 0px 3px 10px 0px lightgray;

  .date-picker-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;

    h2 {
      font-weight: bold;
      font-size: 1.5rem;
    }

    button {
      background-color: #fff;
      padding: 10px 10px;
      border: lightgray solid 1px;
    }
  }

  .seven-days {
    ul {
      display: flex;

      li {
        flex: 1;
        text-align: center;
        padding: 10px 0;
      }
    }
  }

  .months-wrapper {
    overflow: hidden;

    .month-mover {
      display: flex;

      .month {
        min-width: 100%;
        background-color: #fff;
        display: flex;
        flex-wrap: wrap;
        align-content: flex-start;
        margin: 0 20px;
        transform: translateX(-60px);

        li {
          width: 14.2857142857%;
          font-size: 1rem;
          display: flex;
          justify-content: center;
          align-items: center;
          border: lightgray solid 1px;
          background-color: #fff;
          cursor: pointer;
          transition: backgroundColor 0.1s linear;

          &:hover {
            background-color: lightgray;
          }
        }
      }
    }
  }
}
</style>
