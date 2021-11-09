<template>
  <div class="m-3">
    <b-form-input
      type="text"
      @keyup.enter="searchKeyword"
      placeholder="Enter keyword..."
    />
  </div>
</template>

<script>
export default {
  name: "TheSearchBar",
  methods: {
    searchKeyword(event) {
      const keyword = event.target?.value.trim();
      if (keyword) {
        this.$emit("search-keyword", keyword);
      }
    },
  },
};
</script>