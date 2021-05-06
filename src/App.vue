<template>
  <div class="wrapper">
    <header>
      <div class="navbar">
        <div class="container">
          <div class="navbar-content">
            <div class="logo">GitHub Finder</div>
          </div>
        </div>
      </div>
    </header>
    <router-view></router-view>
  </div>
</template>

<style lang="scss">

</style>

<script>
export default {
  data() {
    return {
      links: [
        {
          title: "Home",
          url: "/",
        },
      ],
    };
  },
};
</script>
