<template>
  <Datepicker
    v-model="date"
    :action-row-component="actionRow"
    monthNameFormat="long"
    format="dd.MM.yyyy"
    :clearable="false"
    ref="dp"
  >
    <template #input-icon>
      <img
        class="input-slot-image"
        src="data:image/svg+xml,%3Csvg width='24' height='24' viewBox='0 0 24 24' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M19.5 3.75H4.5C4.08579 3.75 3.75 4.08579 3.75 4.5V19.5C3.75 19.9142 4.08579 20.25 4.5 20.25H19.5C19.9142 20.25 20.25 19.9142 20.25 19.5V4.5C20.25 4.08579 19.9142 3.75 19.5 3.75Z' stroke='%23595A5B' stroke-width='1.5' stroke-linecap='round' stroke-linejoin='round'/%3E%3Cpath d='M16.5 2.25V5.25' stroke='%23595A5B' stroke-width='1.5' stroke-linecap='round' stroke-linejoin='round'/%3E%3Cpath d='M7.5 2.25V5.25' stroke='%23595A5B' stroke-width='1.5' stroke-linecap='round' stroke-linejoin='round'/%3E%3Cpath d='M3.75 8.25H20.25' stroke='%23595A5B' stroke-width='1.5' stroke-linecap='round' stroke-linejoin='round'/%3E%3C/svg%3E%0A"
      />
    </template>
  </Datepicker>
</template>

<script>
import { ref, defineAsyncComponent, computed } from 'vue';
import Datepicker from '@vuepic/vue-datepicker';
const ActionRow = defineAsyncComponent(() => import('./ActionRowCustom.vue'));

export default {
  components: { Datepicker },

  setup() {
    const date = ref(new Date());
    const dp = ref();
    // In case of a range picker, you'll receive [Date, Date]
    const format = (date) => {
      const day = date.getDate();
      const month = date.getMonth() + 1;
      const year = date.getFullYear();

      return `${day}.${month}.${year}`;
    };
    const selectDate = () => {
      dp.value.selectDate();
    };
    const closeMenu = () => {
      dp.value.closeMenu();
    };
    const actionRow = computed(() => ActionRow);
    return {
      date,
      dp,
      format,
      selectDate,
      closeMenu,
      actionRow,
    };
  },
};
</script>

<style lang="scss" scopped>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,400;0,500;0,600;0,700;1,200&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500&display=swap');
$dp__border_radius: 4px !default;
$dp__cell_border_radius: 50% !default;
$dp__cell_size: 40px !default;
$dp__button_height: 40px !default; // size for buttons in overlays
$dp__month_year_row_height: 40px !default; // height of the month-year select row
$dp__menu_min_width: 330px !default;
$dp__font_family: Inter;
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

.dp__selection_preview {
  appearance: none !important;
}
.dp__arrow_top,
.dp__button {
  appearance: none !important;
  display: none !important;
}
.dp__menu {
  padding: 20px 16px;
  box-shadow: 0px 4px 16px rgba(0, 0, 0, 0.13);
  border-radius: 8px;
}
.dp__input_wrap {
  width: 200px !important;
}
.dp__input_icon {
  left: 150px;
  right: 0;
  transform: translateY(-50%);
  color: var(--dp-icon-color);
}
.dp__input_icon_pad {
  padding-left: 20px;
  padding-right: 35px;
}
.slot-icon {
  height: 24px;
  width: auto;
  margin-left: 5px;
}
</style>
