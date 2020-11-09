<template>
  <div class="container mx-auto my-8 max-w-3xl p-5">
    <h1 class="text-5xl font-extrabold leading-none mb-4">
      ⚠️ Register a CEX Offender
    </h1>
    <p class="text-2xl font-light leading-snug">
      Crypto is rife with centralized exchanges that scam users and projects alike. This site accepts anonymous tips on their unethical practices.
    </p>
    <div class="mt-6 mb-8 border-b border-gray-200">
      <nav class="-mb-px flex">
        <g-link
          to="/"
          class="whitespace-no-wrap ml-8 py-4 px-1 border-b-2 font-medium text-sm leading-5 focus:outline-none focus:text-indigo-800 focus:border-indigo-700"
          exact-active-class="border-indigo-500 text-indigo-600"
        >
          Submit
        </g-link>
        <g-link
          to="/submissions"
          class="whitespace-no-wrap ml-8 py-4 px-1 border-b-2 font-medium text-sm leading-5 focus:outline-none focus:text-indigo-800 focus:border-indigo-700"
          exact-active-class="border-indigo-500 text-indigo-600"
        >
          Registered
        </g-link>
        <g-link
          to="/pending"
          class="whitespace-no-wrap ml-8 py-4 px-1 border-b-2 font-medium text-sm leading-5 focus:outline-none focus:text-indigo-800 focus:border-indigo-700"
          exact-active-class="border-indigo-500 text-indigo-600"
        >
          Pending
        </g-link>
      </nav>
    </div>

    <slot />

    <footer
      class="mt-10 text-gray-700 text-sm text-center border-t-2 border-gray-200 pt-5"
    >
      Made by the usual suspects
    </footer>
  </div>
</template>

<script>
import ExternalLink from "~/components/ExternalLink";

export default {
  components: {
    ExternalLink,
  },
};
</script>
