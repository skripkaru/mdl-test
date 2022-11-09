<template>
  <label class="radio">
    <input
      type="radio"
      :name="name"
      :value="value"
      :checked="value === modelValue"
      @change="$emit('update:modelValue', $event.target.value)"
    />
    <span class="radio__indicator"/>
    <span class="radio__label">{{ label }}</span>
  </label>
</template>

<script>
export default {
  name: "Radio",
  props: {
    name: {
      type: String,
    },
    label: {
      type: String,
    },
    value: {
      type: String,
      default: null,
    },
    modelValue: {
      type: String,
      default: null,
    },
  }
}
</script>

<style lang="scss" scoped>
.radio {
  display: inline-flex;
  align-items: center;

  input {
    position: absolute;
    z-index: -1;
    opacity: 0;
  }

  &__label {
    color: var(--color-text-500);
    cursor: pointer;
    transition: color .3s ease-in-out;
  }

  input:checked ~ .radio__indicator:before {
    border-color: var(--color-primary-500);
  }

  input:checked ~ .radio__indicator:after {
    opacity: 1;
    visibility: visible;
  }

  input:checked ~ .radio__label {
    color: var(--color-text-800);
  }

  input:disabled ~ .radio__indicator:before {
    border-color: var(--color-text-300);
    background-color: var(--color-text-300);
  }

  input:disabled ~ .radio__label {
    color: var(--color-text-300);
  }

  &__indicator {
    position: relative;
    width: 18px;
    height: 18px;
    border-radius: 50%;
    padding-left: 1rem;
    margin-right: .5rem;
    cursor: pointer;

    &:before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      display: inline-block;
      width: 100%;
      height: 100%;
      border: 2px solid var(--color-text-500);
      border-radius: 50%;
      transition: border-color .3s, background-color .3s;
    }

    &:after {
      content: '';
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 10px;
      height: 10px;
      border-radius: 50%;
      background-color: var(--color-primary-500);
      opacity: 0;
      visibility: hidden;
      transition: opacity .3s, visibility .3s;
    }
  }
}
</style>