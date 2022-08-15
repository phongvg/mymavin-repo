<script>
import { mapState } from "vuex";

import Vertical from "./vertical";

/**
 * Default Layout
 */
export default {
  components: {
    Vertical,
  },
  data() {
    return {};
  },
  computed: mapState(["layout"]),
  mounted() {
    if (this.$route.query.layout) {
      this.$store.dispatch("layout/changeLayoutType", {
        layoutType: this.$route.query.layout,
      });
    }
  },
};
</script>

<template>
  <div>
    <!-- Begin page -->
    <Vertical
      v-if="layout.layoutType === 'vertical'"
      :layout="layout.layoutType"
    >
      <Nuxt />
    </Vertical>
    <!-- END layout-wrapper -->
  </div>
</template>
