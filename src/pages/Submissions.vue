<template>
  <Layout>
    <SubmissionList title="Registered CEX Offenders" :submissions="submissions">
      Submissions appear here once verified and pull request merged.
    </SubmissionList>
  </Layout>
</template>

<page-query>
  query {
    submissions: allSubmission {
      edges {
        node {
          id
          date
          description
          name
          title
        }
      }
    }
  }
</page-query>

<script>
import SubmissionList from "~/components/SubmissionList";

export default {
  components: {
    SubmissionList,
  },
  metaInfo: {
    title: "Registered CEX Offenders",
  },
  computed: {
    submissions() {
      return this.$page.submissions.edges.map((e) => e.node);
    },
  },
};
</script>

<style lang="scss" scoped></style>
