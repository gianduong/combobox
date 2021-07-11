<template>
  <div class="contain">
    <h1 class="Combobox">Combobox</h1>
    <Combobox
      style="width: 200px"
      :value.sync="valueCombobox"
      :suggestions="[
        { value: 10, text: '10 bản ghi trên trang' },
        { value: 20, text: '20 bản ghi trên trang' },
        { value: 30, text: '30 bản ghi trên trang' },
        { value: 50, text: '50 bản ghi trên trang' },
        { value: 100, text: '100 bản ghi trên trang' },
      ]"
    />

    <h1 class="Autocomplete">ComboboxAutocomplete</h1>
    <ComboboxAutoComplete
      style="width: 300px"
      :value="valueAutoComplete"
      :suggestions="[
        { value: 1, text: 'Bộ phận kho' },
        { value: 2, text: 'Bộ phận Marketing' },
        { value: 3, text: 'Bộ phận nhân sự' },
        { value: 4, text: 'Bộ phận tài chính' },
        { value: 5, text: 'Bộ phận quản lý' },
      ]"
    />
  </div>
</template>

<script>
import ComboboxAutoComplete from "../components/common/ComboboxAutoComplete.vue";
import Combobox from "../components/common/Combobox.vue";
export default {
  name: "Test",
  props: {},
  components: {
    Combobox,
    ComboboxAutoComplete,
  },
  data() {
    return {
      // gia tri duoc chon cua du lieu
      valueAutoComplete: 3,
      // gia tri duoc chon cua du liệu
      valueCombobox: 10,
    };
  },
};
</script>

<style lang="scss" scoped>
.contain {
  border: 1px solid #cccccc;
  background: #f0f0f0;
  box-sizing: border-box;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  margin-top: 100px;
  padding-bottom: 200px;
  padding-top: 200px;
}

h1 {
  margin: 15px;
  color: rgb(0, 255, 76);
  font-size: 30px;
}
</style>