<template>
  <div class="app">
    <Test />
  </div>
</template>

<script>
import Test from "./components/Test.vue";
export default {
  name: "App",
  components: {
    Test,
  },
};
</script>

<style lang="scss">
// #app {
//   font-family: Avenir, Helvetica, Arial, sans-serif;
//   -webkit-font-smoothing: antialiased;
//   -moz-osx-font-smoothing: grayscale;
//   text-align: center;
//   color: #2c3e50;
//   margin-top: 60px;
// }

// Biến chung.
$navbar-width: 178px;
$navbar-width-toggle: 52px;

$header-height: 48px;

$icon-size: 24px;

$color-white: #fff;

// mixins
@mixin flex-row {
  display: flex;
  flex-direction: row;
}

@mixin icon-default {
  background-image: url("./assets/Sprites.64af8f61.svg");
  background-repeat: no-repeat;
  display: inline-block;
}

@mixin icon-bind($position, $size: $icon-size) {
  background-position: $position;
  height: $size;
  width: $size;
}

.flex-row-align-center {
  @include flex-row();
  align-items: center;
}

// style chung
* {
  box-sizing: border-box;
  font-family: inherit;
  font-size: inherit;
}

html,
body {
  margin: 0;
  padding: 0;
  font-size: 13px;
  font-family: NotoSans;
  overflow-y: auto;
  scroll-behavior: smooth;
}

a {
  text-decoration: none;
}

// Icon
.icon {
  @include icon-default();

  &.icon-arrow-dropdown {
    @include icon-bind(-560px -359px, 16px);
  }
}

// input
.input {
  height: 32px;
  outline: none;
  border: 1px solid #ccc;
  padding-left: 12px;
  width: 100%;

  &::placeholder {
    font-style: italic;
  }

  &:focus {
    border-color: #2ca01c;
  }

  &:hover:not(:focus) {
    border-color: #888b8f;
  }

  &.has-icon {
    padding-right: 28px;
  }

  &.has-error {
    border-color: #f20 !important;
  }
}

.con-input {
  position: relative;

  .text-error {
    display: none;
  }

  &:hover .text-error {
    white-space: nowrap;
    display: inline-block;
    position: absolute;
    top: 100%;
    left: 0;
    background-color: #38393d;
    color: $color-white;
    padding: 8px;
    z-index: 10;
  }

  .icon-input {
    position: absolute;
    right: 8px;
    top: 8px;
  }
}

.label-input {
  display: inline-block;
  margin-top: 8px;
  margin-bottom: 4px;
  font-weight: bold;
}

// dropdown
.dropdown {
  position: relative;

  .dropdown-content {
    min-width: 100%;
    position: absolute;
    background-color: $color-white;
    border: 1px solid #ccc;
    white-space: nowrap;
    z-index: 20;
    min-width: 100%☺;

    &.reserve {
      top: auto;
      bottom: 100%;
    }

    &.hide {
      display: none;
    }

    &.right {
      right: 0;
    }
    .dropdown-item-empty {
      background-color: #f7f7f7;
      color: #575757;
      height: 40px;
      line-height: 40px;
      padding-left: 12px;
      padding-right: 12px;
      text-align: center;
      border: 1px solid rgb(197, 197, 197);
    }

    .dropdown-item {
      height: 32px;
      line-height: 32px;
      padding-left: 12px;
      padding-right: 12px;
      cursor: pointer;

      &:hover:not(.active) {
        background-color: #f4f5f6;
        color: #2ca01c;
      }
    }
  }
}

// autocomplete
.autocomplete {
  .icon-dropdown-box {
    cursor: pointer;
    height: 30px;
    width: 30px;
    top: 1px;
    right: 1px;
    display: flex;
    align-items: center;
    justify-content: center;

    &:hover {
      background-color: #e9e9e9;
      border-left: none;
      border-top-right-radius: 4px;
      border-end-end-radius: 4px;
    }
  }

  .active {
    background-color: rgb(0, 255, 76);;
    color: $color-white;
  }
}
</style>
