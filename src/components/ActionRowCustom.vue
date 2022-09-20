<template>
  <div class="custom-action-row">
    <!-- <p class="current-selection">{{ date }}</p> -->
    <button class="cancel-button" @click="$emit('closePicker')">Cancel</button>
    <button class="select-button" @click="$emit('selectDate')">Ready</button>
  </div>
</template>

<script>
import { computed, defineComponent } from 'vue';

export default defineComponent({
  emits: ['selectDate', 'closePicker'],
  props: {
    selectText: { type: String, default: 'Select' },
    cancelText: { type: String, default: 'Cancel' },
    internalModelValue: { type: [Date, Array], default: null },
    range: { type: Boolean, default: false },
    previewFormat: {
      type: [String, Function],
      default: () => '',
    },
    monthPicker: { type: Boolean, default: false },
    timePicker: { type: Boolean, default: false },
  },
  setup(props) {
    const date = computed(() => {
      if (props.internalModelValue) {
        const date = props.internalModelValue.getDate();
        const month = props.internalModelValue.getMonth() + 1;
        const year = props.internalModelValue.getFullYear();
        const hours = props.internalModelValue.getHours();
        const minutes = props.internalModelValue.getMinutes();

        return `${month}/${date}/${year}, ${hours}:${minutes}`;
      }
      return '';
    });

    return {
      date,
    };
  },
});
</script>

<style lang="scss">
.custom-action-row {
  display: flex;
  align-items: center;
  justify-content: center;
  column-gap: 16px;
  margin-top: 24px;
}

.current-selection {
  margin: 10px 0 0 0;
}

.select-button,
.cancel-button {
  border: none;
  background: transparent;
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 500;
  font-size: 14px;
  line-height: 17px;
  text-align: center;
  letter-spacing: 0.4px;
  color: #ffffff;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  padding: 10px 50px;
  gap: 8px;

  border-radius: 5px;
}
.select-button {
  background: #000000;
  border: 1px solid #000000;
}
.cancel-button {
  background: transparent;
  border: 1px solid #9b9b9b;
  color: #9b9b9b;
}
</style>
