<template>
  <div id="app">
    <header>
      <h1>
        {{ title }}
      </h1>
    </header>
    <component :is="page" />
  </div>
</template>

<script>
import Poll from './components/Poll.vue'

export default {
  name: 'App',
  data: () => ({
    page: null,
    title: null,
  }),
  created() {
    const pathname = window.location.pathname.slice(1)
    this.page = () =>
      import(`./content/${pathname || 'index'}.md`).then(
        ({ attributes, vue }) => {
          this.title = attributes.title
          return { extends: vue.component, components: { Poll } }
        }
      )
  },
}
</script>

<style>
@import 'https://newcss.net/lite.css';
:root {
  --nc-bg-1: #2d3748;
  --nc-bg-2: #1a202c;
}
</style>
