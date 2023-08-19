<template>
  <nav class="navbar expand-lg fixed-top shadow-sm">
    <div class="container">
      <a class="navbar-brand mx-lg-0 mx-auto" href="#">
        <img
          src="../../assets/logo.png"
          alt="Logo"
          width="50"
          height="50"
          class="d-inline-block align-text-center"
        />
        Note List
      </a>
    </div>
  </nav>
</template>

<script>
export default {};
</script>

<style scoped>
.navbar {
  width: 100%;
  height: 70px;
  background-color: #4c0bce;
  box-shadow: rgba(17, 17, 26, 0.1) 0px 0px 16px;
}

.navbar .navbar-brand {
  font-size: 32px;
  font-weight: 500;
  font-style: normal;
  line-height: 1;
  letter-spacing: 1px;
  text-transform: capitalize;
  user-select: none;
  color: #fafafa;
}

.navbar .navbar-brand:hover {
  color: #fafafa;
}
</style>
