<template>
  <calendar-view v-slot="{ event }" :events="russianHolidays">
    <!-- Используя слот требуется вывести список праздников соответствующего дня в каждой ячейке -->
    <!-- Каждый праздник - div.holiday -->
    <!-- Вместо 0 должен быть месяц, а вместо 1 - день, некоторым образом полученные из параметров слота -->
    <!-- Не обязательно явно передавать месяц и день, можно передать данные в любом удобном виде -->
    <div class="holiday">
      {{ event.holiday }}
    </div>
  </calendar-view>
</template>

<script>
import CalendarView from './CalendarView';

export default {
  name: 'RussianHolidaysCalendar',

  components: {
    CalendarView,
  },

  data() {
    return {
      russianHolidays: [
        { date: 1, month: 0, holiday: "New Year's Day" },
        { date: 4, month: 0, holiday: 'New Year Holiday' },
        { date: 5, month: 0, holiday: 'New Year Holiday' },
        { date: 6, month: 0, holiday: 'New Year Holiday' },
        { date: 7, month: 0, holiday: 'Orthodox Christmas Day' },
        { date: 8, month: 0, holiday: 'New Year Holiday' },
        { date: 14, month: 0, holiday: 'Old New Year' },
        { date: 14, month: 1, holiday: "Valentine's Day" },
        { date: 23, month: 1, holiday: 'Defender of the Fatherland Day' },
        { date: 27, month: 1, holiday: 'Special Operations Forces Day' },
        { date: 8, month: 2, holiday: "International Women's Day" },
        { date: 11, month: 2, holiday: "Isra and Mi'raj" },
        { date: 20, month: 2, holiday: 'March Equinox' },
        { date: 13, month: 2, holiday: 'Ramadan starts' },
        { date: 1, month: 4, holiday: 'Spring and Labor Day' },
        { date: 2, month: 4, holiday: 'Orthodox Easter Day' },
        { date: 3, month: 4, holiday: 'Day off for Spring and Labor Day' },
        { date: 8, month: 4, holiday: 'Lailat al-Qadr' },
        { date: 9, month: 4, holiday: 'Victory Day' },
        { date: 10, month: 4, holiday: 'Day off for Victory Day' },
        { date: 13, month: 4, holiday: 'Eid al-Fitr' },
        { date: 12, month: 5, holiday: 'Russia Day' },
        { date: 14, month: 5, holiday: 'Day off for Russia Day' },
        { date: 21, month: 5, holiday: 'June Solstice' },
        { date: 20, month: 6, holiday: 'Eid al-Adha' },
        { date: 10, month: 7, holiday: 'Muharram' },
        { date: 1, month: 8, holiday: 'Day of Knowledge' },
        { date: 22, month: 8, holiday: 'September Equinox' },
        { date: 19, month: 9, holiday: "The Prophet's Birthday" },
        { date: 4, month: 10, holiday: 'Unity Day' },
        { date: 21, month: 11, holiday: 'December Solstice' },
      ],
    };
  },
};
</script>

<style scoped>
.holiday {
  font-weight: bold;
  color: var(--red);
}
</style>
