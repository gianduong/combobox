<template>
  <div class="dropdown autocomplete">
    <div class="dropdown-btn con-input">
      <input
        type="text"
        class="input has-icon"
        readonly
        :value="suggestions[current].text"
        @focus="showSuggestion"
        @blur="onBlur"
        @keydown.up.prevent="up"
        @keydown.down.prevent="down"
        @keydown.enter="enter"
      />
      <div
        class="icon-input icon-dropdown-box"
        @mousedown.prevent="toggleSuggestion"
      >
        <div class="icon icon-arrow-dropdown"
        :class="{rotateicon:statusIcon}"
        ></div>
      </div>
    </div>
    <div class="dropdown-content reserve" :class="{ hide: !isShow }">
      <div
        v-for="(suggestion, i) in suggestions"
        :key="i"
        class="dropdown-item"
        :class="{ active: current == i }"
        @click.prevent="clickSuggestion(suggestion, i)"
      >
        {{ suggestion.text }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    suggestions: {
      type: Array,
      required: true,
    },
    value: {
      type: Number,
      default: null,
    },
  },
  data: () => ({
    isShow: false,
    current: 0,
    statusIcon:false,
  }),
  methods: {
    /**
     * Đảo ngược trạng thái popup
     */
    toggleSuggestion() {
      if (this.isShow) {
        this.isShow = false;
        this.statusIcon = false;
        this.$el.querySelector("input").blur();
      } else {
        this.showSuggestion();
      }
    },

    /**
     * Hiển thị popup
     */
    showSuggestion() {
      this.$el.querySelector("input").focus();
      this.isShow = true;
      this.statusIcon = true;
    },

    /**
     * Chọn một suggesstion
     */
    clickSuggestion(suggestion, index) {
      this.current = index;
      this.isShow = false;
    },

    /**
     * Blur input
     */
    onBlur() {
      setTimeout(() => {
        this.isShow = false;
        this.statusIcon = false;
      }, 200);
    },

    /**
     * Nhấn enter
     */
    enter() {
      this.isShow = false;
      this.$el.querySelector("input").blur();
    },

    /**
     * Nhấn up
     */
    up() {
      if (this.current > 0) this.current--;
    },

    /**
     * Nhấn down
     */
    down() {
      if (this.current < this.suggestions.length - 1) this.current++;
    },
  },

  mounted() {
    let index = this.suggestions.findIndex((s) => s.value == this.value);
    if (index >= 0) {
      this.current = index;
    } else {
      this.current = 0;
    }
  },
};
</script>
<style lang="scss" scoped>
.dropdown-content {
  margin-bottom: 5px;
}
</style>