<template>
  <section class="admin-page-container">
    <img @click="onBack" class="amin-page-img-back" src="../../public/img/icons/left-arrow.png" alt="back">
    <user-list :users="users" />
  </section>
</template>

<script>
import {eventBus} from '../services/event-bus.service.js'
import userList from "../components/user-list.cmp";

export default {
  name:'admin-cmp',
  
  computed: {
    users() {
      return this.$store.getters.users;
    }
  },
  created() {
    this.$store.dispatch({
      type: "loadUsers"
    });
    eventBus.$on('delete', userId =>{
      this.$store.dispatch({
        type: "removeUser",
        userId
        });
    });
  },
  methods:{
    onBack(){
      this.$router.push('/artwork');
    }
  },
  components:{
    userList,
  }
}
</script>
