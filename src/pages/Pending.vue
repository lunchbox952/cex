<template>
  <Layout>
    <SubmissionList title="Pending" :submissions="submissions">
      Pending submissions are open
      <ExternalLink
		href="https://github.com/lunchbox952/cex/pulls?q=is%3Apr+is%3Aopen+label%3Asubmission"
        >pull requests</ExternalLink
      > awaiting verification.
    </SubmissionList>
  </Layout>
</template>

<page-query>
  query {
    github {
      repository(owner: "lunchbox952", name: "cex") {
        pullRequests(last: 100, labels: "submission", states: OPEN) {
          edges {
            node {
              id
              body
              createdAt
            }
          }
        }
      }
    }
  }
</page-query>

<script>
import ExternalLink from "~/components/ExternalLink";
import SubmissionList from "~/components/SubmissionList";

export default {
  components: {
    ExternalLink,
    SubmissionList,
  },
  metaInfo: {
    title: "Registered CEX Offenders",
  },
  computed: {
    submissions() {
      return this.$page.github.repository.pullRequests.edges.map((e) => {
        const [_, title, name, description] = e.node.body.match(
          /# (.+)\n## by (.+)\n> ((.|\n)+)/
        );

        return {
          id: e.node.id,
          date: e.node.createdAt,
          description,
          name,
          title,
        };
      });
    },
  },
};
</script>

<style lang="scss" scoped></style>
