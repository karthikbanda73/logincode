<template>
  <section>
    <div class="row at-row flex-center flex-middle">
      <div class="col-lg-24">
        <a href="/"><img class="super-justice" :src="headerImage"></a>
      </div>
    </div>
    <div class="row at-row flex-center flex-middle">
      <div class="col-lg-24">
        <h1 class="super-header">{{subtitle}}</h1>
      </div>
    </div>
    <div class="row at-row flex-center flex-middle">
      <div class="col-lg-3">
      </div>
	  <div class="col-lg-6">
    <label for="uname"><b>UID</b></label>
    <input type="text" placeholder="Enter Username" name="uname" required>

    <label for="psw"><b>Password</b></label>
    <input type="password" placeholder="Enter Password" name="psw" required>

    <button type="submit">Login</button>
    <label>
      <input type="checkbox" checked="checked" name="remember"> Remember me
    </label>
  </div>

      <div class="col-lg-3">
      </div>
    </div>
    <div class="row at-row flex-center flex-middle">
      <div class="col-lg-24">
      </div>
      </div>
  </section>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      headerImage: "",
      subtitle: "",
      errors: []
    };
  },
  created() {
    axios.get("/api/sites/" + process.env.SITE_CODE)
      .then(response => {
        var page = response.data.payload.pages.Home
        document.title = page.title
        this.headerImage = page.headerImage
        this.subtitle = page.subtitle
      }).catch(e => {
        this.errors.push(e)
      })
  },
  methods: {
    link(rel) {
      this.$router.push({ name: rel });
    }
  }
};
</script>