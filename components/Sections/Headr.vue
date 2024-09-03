<template>
  <header>
    <div
      class="container mx-auto px-8 py-4 md:px-12 md:py-10 flex items-center min-h-screen max-w-6xl"
    >
      <main v-if="about">
        <p class="mb-4 font-sourcecode text-blue-500 dark:text-cyan-400">
          Hi, my name is
        </p>
        <h1 class="text-6xl md:text-7xl lg:text-8xl font-light">
          {{ about.name }}
        </h1>
        <h2
          class="text-6xl md:text-7xl lg:text-8xl font-bold text-gray-500 dark:text-gray-400"
        >
          {{ about.title }}
        </h2>
        <p class="mt-4 max-w-lg text-gray-500 dark:text-gray-400 leading-7">
          {{ about.bio }}
        </p>
        <nuxt-link
          to="/#contact"
          class="mt-8 px-6 py-3 font-sourcecode text-white dark:text-cyan-400 inline-block border-2 bg-blue-500 border-blue-500 dark:border-cyan-400 rounded-md transition hover:bg-blue-500 dark:hover:bg-cyan-400 hover:bg-opacity-80 dark:hover:bg-opacity-20 focus:bg-blue-500 dark:focus:bg-cyan-400 focus:bg-opacity-20 dark:focus:bg-opacity-20 focus:outline-none"
        >
          Get In Touch
        </nuxt-link>
        <a
          href="/resume-andika-rahmat-moranda.pdf"
          class="mt-8 px-6 py-3 font-sourcecode text-blue-500 dark:text-cyan-400 inline-block border-2 border-blue-500 dark:border-cyan-400 rounded-md transition hover:bg-blue-500 dark:hover:bg-cyan-400 hover:bg-opacity-20 dark:hover:bg-opacity-20 focus:bg-blue-500 dark:focus:bg-cyan-400 focus:bg-opacity-20 dark:focus:bg-opacity-20 focus:outline-none"
          target="_blank"
        >
          Resume
        </a>
      </main>
    </div>
  </header>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Headr',
  data() {
    return {
      about: {},
    }
  },
  created() {
    this.getAbout()
  },
  methods: {
    async getAbout() {
      const about = await this.$content('about').fetch()

      this.about = about
    },
  },
}
</script>
