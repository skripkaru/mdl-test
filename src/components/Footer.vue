<template>
  <footer class="footer">
    <p>
      2020-2022
      <a class="footer__link" href="#">Terms of Service</a>
      and
      <a class="footer__link" href="#">Conditions</a>
    </p>
  </footer>
</template>

<script>
export default {
  name: "Footer"
}
</script>

<style lang="scss" scoped>
.footer {
  flex: 0 0 auto;
  padding: 1.5rem 2rem;
  font-family: 'Montserrat', sans-serif;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  color: var(--color-text-500);

  &__link {
    position: relative;
    display: inline-block;
    color: var(--color-primary-700);
    text-decoration: none;

    &:after {
      content: '';
      display: block;
      width: 100%;
      height: 1px;
      background-color: var(--color-primary-700);
      opacity: .2;
      transition: opacity .3s ease-in-out;
    }

    &:hover {

      &:after {
        opacity: 0;
      }
    }
  }
}
</style>