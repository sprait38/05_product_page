<!-- eslint-disable max-len -->
<template>
  <component :is="currentPageComponent" :page-params="currentPageParams"/>
</template>

<script>
import MainPageVue from './page/MainPage.vue';
import ProductPageVue from './page/ProductPage.vue';
import NotFoundPageVue from './page/NotFoundPage.vue';
import eventBus from './eventBus';

const routes = {
  main: 'MainPageVue',
  product: 'ProductPageVue',
};

export default {
  data() {
    return {
      currentPage: 'main',
      currentPageParams: {},
    };
  },
  methods: {
    gotoPage(pageName, pageParams) {
      this.currentPage = pageName;
      this.currentPageParams = pageParams || {};
    },
  },
  computed: {
    currentPageComponent() {
      return routes[this.currentPage] || 'NotFoundPage';
    },
  },
  components: { MainPageVue, ProductPageVue, NotFoundPageVue },
  created() {
    eventBus.$on('gotoPage', (pageName, pageParams) => this.gotoPage(pageName, pageParams));
  },
};
</script>
