<template>
  <section id="projects" class="relative">
    <div
      v-if="projects"
      class="container mx-auto px-8 py-4 md:px-20 md:py-10 max-w-6xl"
    >
      <h1
        class="mb-5 md:mb-10 text-3xl md:text-4xl font-bold text-center whitespace-nowrap"
      >
        Projects
      </h1>
      <article
        v-for="(project, index) in projects"
        :key="(index + 1) * Math.random()"
        class="mx-auto mb-8 md:mb-12 relative lg:flex lg:items-center rounded-xl overflow-hidden"
        :class="{
          'text-right flex-row': index % 2 === 0,
          'text-left flex-row-reverse': index % 2 !== 0,
        }"
      >
        <div
          class="h-80 relative w-full lg:max-w-2xl rounded-xl overflow-hidden shadow-xl"
        >
          <div
            class="hidden lg:block absolute inset-0 bg-blue-500 dark:bg-gray-800 bg-opacity-50 dark:bg-opacity-50 transition duration-300 hover:bg-opacity-0 dark:hover:bg-opacity-0"
          ></div>
          <img
            :src="project.cover_image"
            :alt="project.name"
            loading="lazy"
            class="h-full w-full object-cover"
          />
        </div>
        <div
          class="p-4 md:p-6 lg:p-0 flex items-center absolute text-gray-200 lg:text-gray-900 lg:dark:text-gray-200 bg-blue-900 bg-opacity-90 dark:bg-green-900 dark:bg-opacity-90 inset-0 lg:relative lg:bg-transparent lg:dark:bg-transparent z-10"
          :class="{
            'lg:-ml-12 lg:-mr-0': index % 2 === 0,
            'lg:-ml-0 lg:-mr-12': index % 2 !== 0,
          }"
        >
          <div>
            <p class="font-sourcecode text-blue-400 dark:text-cyan-400 rounded">
              Featured
            </p>
            <h2
              class="mb-2 md:mb-4 font-bold text-xl md:text-3xl tracking-tight"
            >
              {{ project.name }}
            </h2>
            <div
              class="lg:p-4 lg:bg-gray-100 lg:dark:bg-gray-800 lg:shadow-xl lg:rounded-lg"
            >
              <p class="leading-7">
                {{ trimDescription(project.description) }}
                <button
                  v-if="trimDescription(project.description).length > 135"
                  class="text-blue-500 dark:text-cyan-400 underline"
                  @click="openModal(project)"
                >
                  Read more
                </button>
              </p>
            </div>
            <p
              class="mt-2 md:mt-4 font-sourcecode text-gray-200 lg:text-gray-500 lg:dark:text-gray-400 rounded"
            >
              <span
                v-for="(lang, i) in project.languages"
                :key="(i + 1) * Math.random()"
              >
                {{ lang }}
              </span>
            </p>
            <div
              class="mt-2 md:mt-4 text-lg text-gray-200 lg:text-gray-500 lg:dark:text-gray-400 flex items-center"
              :class="{
                'justify-end': index % 2 === 0,
              }"
            >
              <!-- <a
                :href="project.github_link"
                target="_blank"
                rel="noreferrer"
                class="h-8 w-8 grid place-items-center hover:text-blue-500 focus:text-blue-500 dark:hover:text-cyan-400 dark:focus:text-cyan-400 rounded-full ring-blue-500 dark:ring-cyan-500 focus:ring-2 focus:outline-none"
              >
                <git-hub class="h-2/3 w-2/3" />
              </a> -->
              <a
                :href="project.live_link"
                target="_blank"
                rel="noreferrer"
                class="h-8 w-8 grid place-items-center hover:text-blue-500 focus:text-blue-500 dark:hover:text-cyan-400 dark:focus:text-cyan-400 rounded-full ring-blue-500 dark:ring-cyan-500 focus:ring-2 focus:outline-none"
              >
                <external-link class="h-2/3 w-2/3" />
              </a>
            </div>
          </div>
        </div>
      </article>
    </div>
  </section>
</template>

<script>
import { mapActions } from 'vuex'
import ExternalLink from '../Icons/ExternalLink.vue'
// import GitHub from '../Icons/GitHub.vue'

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Project',
  components: { ExternalLink },
  data() {
    return {
      projects: [],
    }
  },
  created() {
    this.getProjects()
  },
  methods: {
    ...mapActions({
      openModal: 'openModal',
    }),
    async getProjects() {
      const projects = await this.$content('projects/featured')
        .sortBy('createdAt')
        .fetch()

      this.projects = projects
    },
    trimDescription(description) {
      const maxLength = 135
      let trimmedDesc

      if (description.length > maxLength) {
        trimmedDesc = `${description.substring(0, maxLength)}...`
      } else {
        trimmedDesc = description
      }

      return trimmedDesc
    },
  },
}
</script>
