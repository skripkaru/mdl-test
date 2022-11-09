<template>
  <div class="select" @blur="closeSelect">
    <div class="select__field" :class="{ isOpen: isOpen }" :tabindex="0" @click="toggleSelect">
      {{ selected }}
      <span class="select__arrow">
        <svg width="12" height="8" viewBox="0 0 12 8" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
          <path d="M1.41 0.579956L6 5.16996L10.59 0.579956L12 1.99996L6 7.99996L0 1.99996L1.41 0.579956Z"/>
        </svg>
      </span>
    </div>
    <ul v-if="isOpen" class="select__options" :class="{ isOpen: isOpen }">
      <li
        class="select__option"
        v-for="option of options"
        :key="option.value"
        @click="selectOption(option)"
      >
        {{ option.label }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "VSelect",
  props: {
    options: {
      type: Array,
      default: []
    },
    placeholder: {
      type: String,
      default: "Select"
    },
  },
  data() {
    return {
      selected: this.options.length > 0 ? this.options[0].label : null,
      isOpen: false,
    }
  },
  methods: {
    toggleSelect() {
      this.isOpen = !this.isOpen
    },
    closeSelect() {
      this.isOpen = false
    },
    selectOption(option) {
      this.selected = option.label
      this.$emit("select", option);
      this.closeSelect()
    }
  },
}
</script>

<style lang="scss" scoped>
.select {
  position: relative;
  width: 100%;
  height: 32px;
  border-radius: 6px;

  &__field {
    padding: 0.5rem 2rem 0.5rem 0.5rem;
    font-size: 0.875rem;
    line-height: 14px;
    color: var(--color-text-800);
    background: var(--color-text-200);
    border: 1px solid var(--color-text-300);
    border-radius: 6px;
    cursor: pointer;
    user-select: none;

    &:focus {
      outline: none;
      border: 1px solid var(--color-primary-500);
    }

    &.isOpen {
      border: 1px solid var(--color-primary-500);

      .select__arrow {
        transform: rotate(180deg);
        color: var(--color-primary-500);
      }
    }
  }

  &__arrow {
    position: absolute;
    top: 4px;
    right: 8px;
    width: 24px;
    height: 24px;
    display: flex;
    justify-content: center;
    align-items: center;
    color: var(--color-text-300);
  }

  &__options {
    margin-top: 1px;
    position: absolute;
    left: 0;
    right: 0;
    background: var(--color-secondary-500);
    box-shadow: 0 4px 4px rgba(0, 0, 0, 0.25);
    border-radius: 6px;
    z-index: 1;
    overflow: hidden;
    display: none;

    &.isOpen {
      display: block;
    }
  }

  &__option {
    padding: 0.5rem;
    font-size: 14px;
    line-height: 16px;
    color: var(--color-text-800);
    cursor: pointer;
    user-select: none;
    transition: background-color .3s ease-in-out;

    &:hover {
      background: var(--color-text-200);
    }
  }
}
</style>