<template>
<div class="dashboard">
  <MyPhotos v-if="user" />
  <Login v-else />
</div>
</template>
<script>
import MyPhotos from '@/components/MyPhotos.vue';
import Login from '@/components/Login.vue';
import axios from 'axios';
export default {
  name: 'dashboard',
  components: {
    MyPhotos,
    Login,
  },
  async created() {
    try {
      console.log("about to check users in dashboard");
      let response = await axios.get('/api/users');
      console.log("got response in dashboard");
      this.$root.$data.user = response.data.user;
    } catch (error) {
      this.$root.$data.user = null;
    }
  },
  computed: {
    user() {
      return this.$root.$data.user;
    }
  }
}
</script>
<style scoped>
.dashboard {
  padding-top: 10px;
}
</style>

