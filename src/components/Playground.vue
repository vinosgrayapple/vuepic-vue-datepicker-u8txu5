<template>
  <div>
    <Datepicker v-model="date" monthNameFormat="long" :format-locale="ru" />
  </div>
</template>

<script>
import { ref } from 'vue';
import Datepicker from '@vuepic/vue-datepicker';
import { uk, ru } from 'date-fns/locale';

export default {
  setup() {
    const date = ref(new Date());
    // In case of a range picker, you'll receive [Date, Date]
    const format = (date) => {
      const day = date.getDate();
      const month = date.getMonth() + 1;
      const year = date.getFullYear();

      return `${day}.${month}.${year}`;
    };

    return {
      date,
      format,
      ru,
    };
  },
};
</script>

<style lang="scss" scopped>
$dp__border_radius: 4px !default;
$dp__cell_border_radius: 50% !default;
$dp__cell_size: 40px !default;
$dp__button_height: 40px !default; // size for buttons in overlays
$dp__month_year_row_height: 40px !default; // height of the month-year select row
@import '@vuepic/vue-datepicker/src/VueDatePicker/style/main.scss';
.dp__theme_light {
  --dp-background-color: #ffffff;
  --dp-text-color: #212121;
  --dp-hover-color: #f3f3f3;
  --dp-hover-text-color: #212121;
  --dp-hover-icon-color: #959595;
  --dp-primary-color: #000;
  --dp-primary-text-color: #f8f5f5;
  --dp-secondary-color: #c0c4cc;
  --dp-border-color: #ddd;
  --dp-menu-border-color: #ddd;
  --dp-border-color-hover: #aaaeb7;
  --dp-disabled-color: #f6f6f6;
  --dp-scroll-bar-background: #f3f3f3;
  --dp-scroll-bar-color: #959595;
  --dp-success-color: #76d275;
  --dp-success-color-disabled: #a3d9b1;
  --dp-icon-color: #959595;
  --dp-danger-color: #ff6f60;
  --dp-highlight-color: rgba(25, 118, 210, 0.1);
}
</style>
