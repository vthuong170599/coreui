<template>
  <div>
    <list-category :listCategory="listCategory" :fields="fields" @getListCategory="fetch"/>
    <b-pagination
      v-if="pages.last_page>1"
      v-model="currentPage"
      :total-rows="pages.total"
      :per-page="pages.per_page"
      @page-click="fetch"
      prev-text="Prev"
      next-text="Next"
    ></b-pagination>
  </div>
</template>
<script>
import axios from "axios";
import ListCategory from "~/components/Category/ListCategory.vue";
const FIELDS = [
  { key: "id", label: "id" },
  { key: "name", label: "name" },
  { key: "desc", label: "desc" },
  { key: "method", label: "method" },
];
export default {
  components: { ListCategory },
  data() {
    return {
      listCategory: [],
      fields: FIELDS,
      pages: {},
      currentPage: 1,
    };
  },
  methods: {
    fetch(e, page) {
      axios
        .get("http://127.0.0.1:8000/api/category?page=" + page, {
          headers: {
            Authorization: `${$nuxt.$auth.getToken("local")}`,
          },
        })
        .then((res) => {
          this.listCategory = res.data.data;
          this.pages = res.data.meta;
        });
    },
  },
  mounted() {
    this.fetch();
  },
};
</script>