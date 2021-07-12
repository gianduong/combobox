<template>
  <div class="dropdown autocomplete">
    <div class="dropdown-btn con-input combobox-style">
      <input
        type="text"
        class="input has-icon"
        :value="valueInput"

        @focus="showSuggestion"
        @blur="onBlur"
        @keydown.up.prevent="up"
        @keydown.down.prevent="down"
        @keydown.enter.prevent="enter"
        @input="onInput"
      />
      <div
        class="icon-input icon-dropdown-box"
        
        @mousedown.prevent="toggleSuggestion"
      >
        <div 
        class="icon icon-arrow-dropdown"
        :class="{rotateicon : statusClick}"
        ></div>
      </div>
    </div>
    <div class="dropdown-content" :class="{ hide: !isShow }">
      <div class="dropdown-item-empty" v-if="suggestionData.length == 0">
        Không có dữ liệu hiển thị
      </div>
      <div
        v-for="(suggestion, index) in suggestionData"
        :key="index"
        class="dropdown-item"
        :class="{ active: current == index }"
        @click.prevent="clickSuggestion(suggestion, index), getIndex(), getValue()"
      >
        {{ suggestion.text }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    /**
     * Danh sách suggestion của autocomplete.
     */
    suggestions: {
      type: Array,
      required: true,
    },

    /**
     * Giá trị khởi tạo cho input
     */
    value: {
      type: Number,
      default: null,
    },
  },
  data: () => ({
    /**
     * Xác định trạng thái popup autocomplete
     */
    isShow: false,

    /**
     * vị trí hiện tại
     */
    current: 0,

    /**
     * Danh sách suggesstion của autocomplete có lọc
     */
    suggestionData: [],

    /**
     * Giá trị của input
     */
    valueInput: "",
    /**
    * bien xoay theo su kien click
    */
    statusClick: false,
  }),
  methods: {
    /**
     * Đảo ngược trạng thái popup
     */
    toggleSuggestion() {
      if (this.isShow) {
        this.isShow = false;
        this.$el.querySelector("input").blur();
      } else {
        this.showSuggestion();
      }
    },
    /**
     * getIndex
     */
    getIndex(){
      console.log('id=' + this.suggestionData[this.current].value);
    },
    /**
     * get Value
     */
    getValue(){
      console.log('value=' + this.suggestionData[this.current].text);
    },
    /**
     * Hiển thị popup
     */
    showSuggestion() {
      this.$el.querySelector("input").focus();
      this.isShow = true;
      this.statusClick = true;
    },                                                                            
    /**
     * Nhấn enter
     */
    enter() {
      this.valueInput = this.suggestionData[this.current].text;
      this.isShow = false;
      this.$el.querySelector("input").blur();
      this.statusClick = false;
    },

    /**
     * Nhấn up
     */
    up() {
      if (this.current > 0) this.current--;
      this.valueInput = this.suggestionData[this.current].text;
    },

    /**
     * Nhấn down
     */
    down() {
      if (this.current < this.suggestions.length - 1) this.current++;
      this.valueInput = this.suggestionData[this.current].text;
    },
    /**
     * Chọn một suggesstion
     */
    clickSuggestion(suggestion, index) {
      this.current = index;
      this.isShow = false;
      this.valueInput = suggestion.text;
      this.statusClick = false;
    },

    /**
     * Blur input
     */
    onBlur() {
      setTimeout(() => {
        this.isShow = false;
        this.statusClick = false;
        this.$emit("blur");
      }, 300);
    },

    /**
     * Nhập vào input
     */
    onInput(e) {
      let val = e.target.value;
      this.valueInput = val;
      this.current = 0;
      if (this.suggestions) {
        this.suggestionData = this.suggestions.filter((s) =>
          s.text.toLowerCase().includes(val.toLowerCase())
        );
        this.isShow = true;

      }
    },
  },

  mounted() {
    this.suggestionData = this.suggestions;
    let index = this.suggestionData.findIndex((s) => s.value == this.value);
    if (index >= 0) {
      this.current = index;
      this.valueInput = this.suggestionData[this.current].text;
    } else {
      this.current = 0;
      this.valueInput = "";
    }
  },
};
</script>
<style lang="scss" scoped>
.dropdown-content{
  margin-top: 5px;
}
</style>