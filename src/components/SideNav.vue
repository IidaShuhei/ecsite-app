<template>
  <div id="adminside" v-if="this.$store.state.loginStatus">
    <div>
      <b-sidebar
        id="sidebar-backdrop"
        bg-variant="dark"
        text-variant="light"
        backdrop
        shadow
      >
        <div class="px-4 mb-5 display-1 font-weight-medium title">
          <h2>Menu</h2>
        </div>
        <v-divider></v-divider>
        <v-list class="py-0 bg-dark" dark tile>
          <v-list-item-group>
            <v-list-item>
              <v-list-item-icon>
                <v-icon> mdi mdi-home</v-icon>
              </v-list-item-icon>
              <v-list-item-content>
                <v-list-item-title @click="toPage('/')" class="text-white"
                  >ホーム</v-list-item-title
                >
              </v-list-item-content>
            </v-list-item>
            <v-list-item>
              <v-list-item-icon>
                <v-icon> mdi mdi-cart-outline</v-icon>
              </v-list-item-icon>
              <v-list-item-content>
                <v-list-item-title 
                  class="text-white" 
                  @click="toPage('/cart')"
                  >買い物かご
                </v-list-item-title>
                <v-list-item-title>{{count}}</v-list-item-title>
              </v-list-item-content>
            </v-list-item>
            <v-list-item>
              <v-list-item-icon>
                <v-icon> mdi mdi-history</v-icon>
              </v-list-item-icon>
              <v-list-item-content>
                <v-list-item-title
                  class="text-white"
                  >購入履歴</v-list-item-title
                >
              </v-list-item-content>
            </v-list-item>
          </v-list-item-group>
        </v-list>
        <Logout :class="logoutClass" />
      </b-sidebar>
    </div>
  </div>
</template>

<script>
import Logout from "@/components/Logout";
export default {
  components:{
    Logout
  },
  data() {
    return {
      logoutClass: ["px-4", "my-5", "fixed-bottom"],
      count:0
    }
  },
  mounted() {
    window.addEventListener("resize", this.abjustLogout);
  },
  methods: {
    toPage(path) {
      this.$router.push(path).catch(err => {err});
    },
  },
  abjustLogout() {
    if (window.innerHeight < 600) {
      this.logoutClass = ["px-4", "my-5"];
    } else {
      this.logoutClass = ["px-4", "my-5", "fixed-bottom"];
    }
  },
};
</script>

<style scoped>
 .title {
    position: absolute;
    left: 50%;  /*親要素を起点に左から50%*/
    transform: translateY(-50%) translateX(-50%); 
 }
</style>