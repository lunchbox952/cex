<template>
  <form @submit.prevent="handleSubmit">
    <h2
      class="text-3xl leading-9 tracking-tight font-extrabold text-gray-900 sm:text-4xl sm:leading-10"
    >
      Submit
    </h2>
    <div class="mt-3 sm:mt-4">
      <p class="text-xl leading-7 text-gray-600">
        Submissions trigger a <ExternalLink
		href="https://github.com/lunchbox952/cex/pulls?q=is%3Apr+is%3Aopen+label%3Asubmission"
        >pull request</ExternalLink
      > which will be displayed in the
        <g-link
          to="/pending"
          class="underline text-indigo-600 hover:text-indigo-900 transition ease-in-out duration-150"
          >Pending</g-link
        >
        tab. Once verified and merged, they appear in the
        <g-link
          to="/submissions"
          class="underline text-indigo-600 hover:text-indigo-900 transition ease-in-out duration-150"
          >Registered CEX Offenders</g-link
        >
        list!
      </p>
    </div>
    <Alert v-if="success" theme="success">
      Form submitted successfully! In a few minutes, it will appear in this site, listed as a pending
      submission.
    </Alert>
    <template v-else>
      <Field id="name" :error="nameError" :value.sync="name">
        Exchange name
      </Field>
      <Field id="title" :error="titleError" :value.sync="title">
        CEO full name
      </Field>
      <Field id="description" :value.sync="description" type="textarea">
        Supporting evidence (provide links where possible)
      </Field>
      <label class="flex text-sm leading-5 text-gray-700 mt-5">
        <input type="checkbox" required class="mt-1 mr-2" />
        I understand this will be hosted in a public
        repository and I have not included any sensitive data of my own.
      </label>
      <Alert v-if="error" theme="error">
        Oops, this is embarassing, but something went wrong while submitting the
        form.
      </Alert>
      <Btn :disabled="loading">
        Submit
      </Btn>
    </template>
  </form>
</template>

<script>
import axios from "axios";

import Alert from "~/components/Alert";
import Btn from "~/components/Btn";
import ExternalLink from "~/components/ExternalLink";
import Field from "~/components/Field";

export default {
  data() {
    return {
      name: "",
      title: "",
      description: "",
      loading: false,
      error: false,
      success: false,
    };
  },
  components: {
    Alert,
    Btn,
    ExternalLink,
    Field,
  },
  computed: {
    nameError() {
      if (this.name && this.invalidString(this.name)) {
        return "Please avoid using special characters";
      }
      return "";
    },
    titleError() {
      if (this.title && this.invalidString(this.title)) {
        return "Please avoid using special characters";
      }
      return "";
    },
  },
  methods: {
    invalidString(str) {
      return !/^(?!.*(#|>))/.test(str);
    },
    handleSubmit() {
      this.loading = true;
      this.error = false;
      this.success = false;
      axios
        .post(process.env.GRIDSOME_LAMBDA, {
          name: this.name,
          title: this.title,
          description: this.description,
        })
        .then(() => {
          this.success = true;
          this.name = "";
          this.title = "";
          this.description = "";
          this.loading = false;
        })
        .catch(() => {
          this.loading = false;
          this.error = true;
        });
    },
  },
};
</script>
