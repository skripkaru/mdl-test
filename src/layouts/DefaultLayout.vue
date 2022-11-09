<template>
  <div class="default-layout">
    <main class="main">
      <slot/>
    </main>
    <Footer/>
  </div>
</template>

<script>
import Footer from "@/components/Footer";

export default {
  name: "DefaultLayout",
  components: {
    Footer,
  }
}
</script>

<style lang="scss" scoped>
.default-layout {
  display: flex;
  flex-direction: column;
  height: 100%;
  width: 100%;
  max-width: 986px;
  margin: 0 auto;
  background: var(--color-text-100) url("~@/assets/bg.png") bottom / contain no-repeat;
}

.main {
  flex: 1 0 auto;
}
</style>