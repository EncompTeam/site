<template>
  <section class="main">
    <div class="main__content" @mouseenter="isMouseOver = true" @mouseleave="isMouseOver = false">
      <img class="main__image" src="/encomp-logo-large.svg" alt="Logo do sexto encomp com detalhes verdes e letras brancas">
      <h1 class="main__text">
        Em breve...
      </h1>
      <NuxtLink class="main__link" target="_blank" external href="https://www.instagram.com/encompceunes/">
        Nos encontre no Instagram
      </NuxtLink>
    </div>
    <div ref="blob" class="blob" :class="isMouseOver ? 'hovered': ''" />
  </section>
</template>
<script setup>
useHead({
  title: 'VI Encomp',
  meta: [
    {
      hid: 'description',
      name: 'description',
      content: 'Em breve...'
    }
  ]
})
const isMouseOver = ref(false)
const { x, y } = useMouse()
const blob = ref(null)
onMounted(() => {
  const el = blob.value
  watch([x, y], ([x, y]) => {
    el.style.transform = `translate(${x - 75}px, ${y - 75}px)`
  })
})
</script>
<style lang="scss">
@import "@/assets/styles/base.scss";

.main {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  background-image: url("/assets/images/texture-bg.png");

  &__content {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 50%;
    height: 50%;
  }

  &__text {
    color: var(--color-white);
    font-size: 3rem;
  }

  &__image{
    width: 100%;
    max-width: 500px;
  }

  &__link {
    color: var(--color-black);
    transition: color 200ms ease-in-out;
    margin-top: 1rem;

    &:hover {
      color: var(--color-white);
    }
  }
}

.blob {
  position: absolute;
  top: 0;
  left: 0;
  width: 0;
  height: 0;
  background-color: var(--color-purple-primary);
  z-index: -1;
  border-radius: 50%;
  opacity: 0.75;
  filter: blur(25px);
  transition: width 200ms ease-in-out, height 200ms ease-in-out;
  display: flex;
  justify-content: center;

  &.hovered {
    width: 150px;
    height: 150px;
  }
}
</style>
