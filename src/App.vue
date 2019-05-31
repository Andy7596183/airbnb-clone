<template>
  <div id="app">
    <Navbar/>
    <router-view/>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar";
export default {
  components: {
    Navbar
  },
  mounted() {
    setTimeout(() => {
      window.fbAsyncInit = function() {
        FB.init({
          appId: "2048396828605759",
          cookie: true,
          xfbml: true,
          version: "v3.3"
        });

        FB.AppEvents.logPageView();
        console.log("fbInit");
      };

      FB.getLoginStatus(function(response) {
        statusChangeCallback(response);
      });
    }, 2000);
  },
  methods: {
    login() {
      let vm = this;
      FB.login(
        function(response) {
          console.log("res", response);
        },
        {
          scope: "email, public_profile",
          return_scopes: true
        }
      );
    }
  }
};
</script>