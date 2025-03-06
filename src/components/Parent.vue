<template>
  <div class="parent">
    <p>Вы выбрали: {{ selectedItem }}</p>
    <drop-down v-model="selectedItem" :items="dropdownItems"></drop-down>
  </div>
</template>

<script>
import DropDown from './DropDown.vue';

export default {
  components: { DropDown },
  data () {
    return {
      dropdownItems: [
        'Item 1',
        'Item 2',
        'Item 3',
        'Item 4',
        'Item 5',
        'Item 6',
        'Item 7',
      ],
      selectedItem: '',
    };
  },
  methods: {
    name () {
      //
    }
  }
};
</script>

<style scoped>
  .parent {
    width: 358px;
    height: 791px;
    background-color: rgb(159, 159, 159);
    padding: 16px;
    border-radius: 5px;
    margin-left: auto;
    margin-right: auto;
    box-sizing: border-box;

  }
</style>