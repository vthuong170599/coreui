<template>
  <div>
    <create-edit-category @sendDataCategory="getDataCategory" />
  </div>
</template>
<script>
import CreateEditCategory from "~/components/Category/CreateEditCategory.vue";
import axios from "axios";
export default {
  components: { CreateEditCategory },
  methods: {
    getDataCategory(data) {
      axios
        .post(
          "http://127.0.0.1:8000/api/category",
          data,
          {
            headers: {
              Authorization: `${$nuxt.$auth.getToken("local")}`,
            },
          }
        )
        .then((res) => {
          this.$router.push("/category");
        });
    },
  },
};
</script>