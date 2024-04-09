<template>
  <Header />
  <h1>Hello {{ name }} Add the new Restaurant</h1>
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
    <button type="button" v-on:click="addRestaurant">
      Add a new Restaurant
    </button>
  </form>
</template>

<script>
import axios from "axios";
import Header from "./Header.vue";

export default {
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
  methods: {
    async addRestaurant() {
      console.warn(this.Restaurant);
      const result = await axios.post("http://localhost:4040/restaurant", {
        name: this.Restaurant.name,
        address: this.Restaurant.address,
        contact: this.Restaurant.contact,
      });
      if (result.status == 201) {
        this.$router.push({ name: "Home" });
      }
      console.warn("result", result);
    },
  },
  components: {
    Header,
  },
  name: "Add-restaurant",
  mounted() {
    let user = localStorage.getItem("user-info");
    this.name = JSON.parse(user).name;
    if (!user) {
      this.$router.push({ name: "SignUp" });
    }
  },
};
</script>
