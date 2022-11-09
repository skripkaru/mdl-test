<template>
  <input
    class="input"
    :type="type"
    :name="name"
    :placeholder="placeholder"
    :value="modelValue"
    @change="$emit('update:modelValue', $event.target.value)"
  />
</template>

<script>
export default {
  name: "Input",
  props: {
    type: {
      type: String,
      default: 'text',
    },
    name: {
      type: String,
      default: '',
    },
    placeholder: {
      type: String,
      default: '',
    },
    modelValue: {
      type: [String, Number],
      default: ''
    },
  }
}
</script>

<style lang="scss" scoped>
.input {
  width: 100%;
  padding: 8px;
  height: 32px;
  font-size: 0.875rem;
  line-height: 14px;
  color: var(--color-text-800);
  background: var(--color-text-200);
  border: 1px solid var(--color-text-300);
  border-radius: 6px;
  transition: box-shadow .3s ease-in-out, border-color .3s ease-in-out;

  &::placeholder {
    font-weight: 300;
    color: var(--color-text-300);
    transition: opacity .3s ease-in-out;
  }

  &:hover {
    box-shadow: inset 0 0 0 100px rgba(0, 0, 0, 0.2);
  }

  &:focus {
    outline: none;
    border-color: var(--color-primary-500);

    &::placeholder {
      opacity: 0;
    }
  }
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  /* display: none; <- Crashes Chrome on hover */
  -webkit-appearance: none;
  margin: 0; /* <-- Apparently some margin are still there even though it's hidden */
}

input[type=number] {
  -moz-appearance:textfield; /* Firefox */
}
</style>