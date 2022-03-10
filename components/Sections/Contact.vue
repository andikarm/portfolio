<template>
  <section id="contact" class="relative">
    <div class="container mx-auto px-8 py-4 md:px-20 md:py-10 max-w-6xl">
      <h2 class="mb-5 md:mb-10 text-3xl md:text-4xl font-bold text-center">
        Get In Touch
      </h2>
      <div class="mx-auto max-w-sm relative">
        <div
          class="mb-4 font-bold text-center"
          :class="{
            'text-cyan-500': status === 'success',
            'text-red-500': status === 'error'
          }"
        >
          <p v-if="status === 'success'">Message sent successfully.</p>
          <p v-if="status === 'error'">
            There was a error submitting the form.
          </p>
        </div>
        <form
          autocomplete="off"
          name="contact"
          method="POST"
          action="/success"
          data-netlify="true"
          data-netlify-honeypot="bot-field"
          @submit.prevent="submitForm"
        >
          <input type="hidden" name="form-name" value="contact" />
          <div class="mb-4">
            <label for="name" class="block">Name</label>
            <input
              id="name"
              v-model="form.name"
              name="name"
              type="text"
              required
              placeholder="First Last"
              class="
                p-2
                block
                w-full
                border-b
                dark:bg-gray-800
                border-gray-300
                dark:border-gray-700
                transition
                focus:border-blue-500
                dark:focus:border-cyan-400
                ring-blue-500
                dark:ring-cyan-500
                focus:ring-2 focus:outline-none
              "
            />
          </div>
          <div class="mb-4">
            <label for="subject" class="block">Subject</label>
            <input
              id="subject"
              v-model="form.subject"
              name="subject"
              type="text"
              required
              placeholder="Inquiry/ Get Quote..."
              class="
                p-2
                block
                w-full
                border-b
                dark:bg-gray-800
                border-gray-300
                dark:border-gray-700
                transition
                focus:border-blue-500
                dark:focus:border-cyan-400
                ring-blue-500
                dark:ring-cyan-500
                focus:ring-2 focus:outline-none
              "
            />
          </div>
          <div class="mb-4">
            <label for="email" class="block">Email</label>
            <input
              id="email"
              v-model="form.email"
              name="email"
              type="email"
              required
              class="
                p-2
                block
                w-full
                border-b
                dark:bg-gray-800
                border-gray-300
                dark:border-gray-700
                transition
                focus:border-blue-500
                dark:focus:border-cyan-400
                ring-blue-500
                dark:ring-cyan-500
                focus:ring-2 focus:outline-none
              "
            />
          </div>
          <div class="mb-4">
            <label for="message" class="block">Message</label>
            <textarea
              id="message"
              v-model="form.message"
              name="message"
              rows="3"
              required
              class="
                p-2
                block
                w-full
                border-b
                dark:bg-gray-800
                border-gray-300
                dark:border-gray-700
                transition
                focus:border-blue-500
                dark:focus:border-cyan-400
                ring-blue-500
                dark:ring-cyan-500
                focus:ring-2 focus:outline-none
              "
            ></textarea>
          </div>
          <button
            type="submit"
            class="
              mx-auto
              mt-6
              px-6
              py-3
              block
              font-sourcecode
              text-blue-500
              dark:text-cyan-400
              border-2 border-blue-500
              dark:border-cyan-400
              rounded-md
              transition
              hover:bg-blue-500
              dark:hover:bg-cyan-400
              hover:bg-opacity-20
              dark:hover:bg-opacity-20
              focus:bg-blue-500
              dark:focus:bg-cyan-400
              focus:bg-opacity-20
              dark:focus:bg-opacity-20
              focus:outline-none
            "
            :class="{ 'pointer-events-none': busy }"
          >
            <span v-if="busy">Sending...</span>
            <span v-if="!busy">Send</span>
          </button>
        </form>
        <div
          class="
            grid
            place-items-center
            absolute
            top-0
            left-0
            bottom-0
            right-0
            bg-white
            dark:bg-gray-800
            bg-opacity-50
            dark:bg-opacity-50
          "
        >
          <p class="text-center bg-white dark:bg-gray-800">
            Under maintenance.
            <a
              href="mailto:andhika422@gmail.com"
              class="
                text-blue-500
                dark:text-red-500
                hover:text-blue-600
                focus:text-blue-600
                dark:hover:text-red-600 dark:focus:text-red-600
                focus:outline-none
              "
            >
              Email me at andhika422@gmail.com </a
            >. Thanks for your patience :)
          </p>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Contact',
  data() {
    return {
      status: null,
      busy: false,
      form: {
        name: null,
        email: null,
        subject: null,
        message: null
      }
    };
  },
  methods: {
    encode(data) {
      const formData = new FormData();

      for (const key of Object.keys(data)) {
        formData.append(key, data[key]);
      }

      return new URLSearchParams(formData).toString();
    },

    submitForm() {
      this.status = null;
      this.busy = true;

      fetch('/', {
        method: 'POST',
        headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
        body: this.encode({
          'form-name': 'contact',
          ...this.form
        })
      })
        .then(() => {
          this.status = 'success';
          this.busy = false;

          this.form.name = null;
          this.form.email = null;
          this.form.subject = null;
          this.form.message = null;
        })
        .catch((err) => {
          this.status = 'error';
          this.busy = false;

          // eslint-disable-next-line no-console
          console.error(err);
        });
    }
  }
};
</script>
