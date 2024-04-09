<template>
  <Header />
  <h1>Hello {{ name }} welcome to Update Restaurant app</h1>
  <form class="register">
    <input
      type="text"
      name="name"
      placeholder="Enter Name"
      v-model="Restaurant.name"
    />
    <input
      type="text"
      name="address"
      placeholder="Enter Address"
      v-model="Restaurant.address"
    />
    <input
      type="text"
      name="contact"
      placeholder="Enter contact"
      v-model="Restaurant.contact"
    />
    <button type="button" v-on:click="Update_restaurant">
      Update Restaurant
    </button>
  </form>
</template>

<script>
import axios from "axios";

import Header from './Header.vue';

export default {
  name:"UpdateRestaurant",
  components:{
    Header
  },
  data() {
    return {
      name: "",
      Restaurant: {
        name: "",
        address: "",
        contact: "",
      },
    };
  },

  async mounted() {
    let user = localStorage.getItem("user-info");
    this.name = JSON.parse(user).name;
    if (!user) {
      this.$router.push({ name: "SignUp" });
    }
    const result = await axios.get("http://localhost:4040/restaurant/"+this.$route.params.id);
    // console.warn(this.$route.params.id);
    console.warn(result.data);
    this.Restaurant=result.data
  },
};
</script>
