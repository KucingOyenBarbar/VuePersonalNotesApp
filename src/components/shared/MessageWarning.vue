<template>
  <div class="d-flex justify-content-center g-2 py-3">
    <p class="text-start text-capitalize text-white-50 fst-normal">
      {{ message }}
    </p>
  </div>
</template>

<script>
export default {
  props: ["message"],
};
</script>

<style></style>
