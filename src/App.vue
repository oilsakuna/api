<template>
  <div id="app">
    <b-navbar id="nav" toggleable="lg" type="dark">
      
      <svg
      
        xmlns="http://www.w3.org/2000/svg"
        width="100"
        height="100"
        fill="currentColor"
        class="bi bi-house-fill"
        viewBox="0 0 16 16"
      >
        <path
          fill-rule="evenodd"
          d="M8 3.293l6 6V13.5a1.5 1.5 0 0 1-1.5 1.5h-9A1.5 1.5 0 0 1 2 13.5V9.293l6-6zm5-.793V6l-2-2V2.5a.5.5 0 0 1 .5-.5h1a.5.5 0 0 1 .5.5z"
        />
        <path
          fill-rule="evenodd"
          d="M7.293 1.5a1 1 0 0 1 1.414 0l6.647 6.646a.5.5 0 0 1-.708.708L8 2.207 1.354 8.854a.5.5 0 1 1-.708-.708L7.293 1.5z"
        />
      </svg>
      <router-link to="/">MANGA</router-link>
      <div >      
    
    
    
</div>

      <!-- Right aligned nav items -->
      <b-navbar-nav class="ml-auto">
        <b-nav-form>
          <b-form-input
            size="sm"
            class="mr-sm-2 col-8"
            placeholder="Search"
            v-model="sh"
          ></b-form-input>
          <b-button
            size="sm"
            class="btn btn-danger"
            type="submit"
            @click="Search()"
            >Search</b-button
          >
        </b-nav-form>
      </b-navbar-nav>
    </b-navbar>
    <router-view />
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      page: 1,
      sh: "",
      mangaList: null,
      url: "https://api.jikan.moe/v3/magazine/1/1",
    };
  },
  methods: {
    Search() {
      const router = this.$router;
      for (let i = 0; i <= this.mangaList.manga.length; i++) {
        if (this.sh == this.mangaList.manga[i].title) {
          alert(this.mangaList.manga[i].title);
          router.push({
            path: `/about/${this.mangaList.manga[i].mal_id}`,
          });
          break;
        } else if (99 == i) {
          router.push({
            path: `/`,
          });
        }
      }
    },
  },
  mounted() {
    axios
      .get(this.url)
      .then((result) => {
        this.mangaList = result.data;
      })
      .catch((err) => {
        console.log(err);
        alert(err);
      });
  },
};
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #5e0cf5;
  background: rgb(245, 148, 193);
}

#nav {
  padding: 40px;
  background: rgb(245, 148, 193);
}

#nav a {
  font-weight: bold;
  color: #0f0f0e;
}

#nav a.router-link-exact-active {
  color: #070707;
}
</style>
