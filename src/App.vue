<template>
  <div id="app">
    <BaseHeader @show-overlay="handelShowSideBar" />
    <router-view />
    <base-footer :handelShowSideBar="isShowSideBar" />
  </div>
</template>

<script>
import BaseHeader from "./components/BaseHeader";
import BaseFooter from "./components/BaseFooter.vue";
export default {
  metaInfo: {
    titleTemplate: "%s - فروشگاه بیت بایت ",
  },
  data: () => ({
    isShowSideBar: false,
  }),
  components: {
    BaseHeader,
    BaseFooter,
  },
  methods: {
    handelShowSideBar(showbtnSlidemenu) {
      this.isShowSideBar = showbtnSlidemenu;
    },
  },
};
</script>

<style>
</style>
