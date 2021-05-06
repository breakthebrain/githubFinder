<template>
  <div class="wrapper-content wrapper-content--fixed">
    <section>
      <div class="container">
        <div class="error" v-if="error" style="margin-bottom: 20px">
          <p>{{ error }}</p>
        </div>

        <search
          :value="search"
          placeholder="Type user name"
          @search="search = $event"
        />

        <button v-if="!repos" class="btn btnPrimary" @click="getRepos">
          Search
        </button>
        <button v-else class="btn btnPrimary" @click="getRepos">
          Search Again!
        </button>

        <div class="repos__wrapper" v-if="repos">
          <div class="repo-item" v-for="repo in repos" :key="repo.id">
            <div class="repos-info">
              <a class="link" :href="repo.html_url" target="_blank">{{
                repo.name
              }}</a>
              <span>{{ repo.stargazers_count }} ⭐</span>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import search from "@/components/Search.vue";
import axios from "axios";

export default {
  components: { search },
  data() {
    return {
      search: "",
      error: null,
      repos: null,
    };
  },
  methods: {
    getRepos() {
      axios
        .get(`https://api.github.com/users/${this.search}/repos`)
        .then((res) => {
          console.log(res);
          this.repos = res.data;
        })
        .catch((err) => {
          console.log(err);
          this.repos = null;
          this.error = "Cant`t find this repos";
        });
    },

    getUser() {
      axios
        .get(`https://api.github.com/users/${this.search}/repos`)
        .then((res) => {
          console.log(res);
          this.repos = res.data;
        })
        .catch((err) => {
          console.log(err);
          this.repos = null;
          this.error = "Cant`t find this repos";
        });
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  align-items: center;
  flex-direction: column;
}
button {
  margin-top: 40px;
}

.repos__wrapper {
  width: 600px;
  margin: 30px 0;
}
.repos-info {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 10px;
  padding: 10px 0;
  border-bottom: 1px solid #dbdbdb;
}
</style>

