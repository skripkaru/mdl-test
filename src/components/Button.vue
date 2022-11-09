<template>
  <button :class="`btn ${variant ? variant : ''}`" :variant="variant">
    <slot/>
  </button>
</template>

<script>
export default {
  name: "Button",
  props: {
    variant: {
      type: String,
      required: true,
    },
  }
}
</script>

<style lang="scss" scoped>
.btn {
  padding: 0.25rem 0.5rem;
  font-weight: 500;
  font-size: 0.875rem;
  line-height: 1.5rem;
  border-radius: 3px;
  cursor: pointer;
  transition: box-shadow .3s ease-in-out;

  &:hover {
    box-shadow: inset 0 0 0 100px rgba(0, 0, 0, 0.2);
  }

  &:focus {
    outline: none;
    box-shadow: 0 0 0 1px var(--color-primary-100);
  }

  &.fill {
    color: var(--color-text-100);
    background: var(--color-primary-500);
  }

  &.outline {
    color: var(--color-primary-700);
    background: var(--color-secondary-500);
  }
}
</style>