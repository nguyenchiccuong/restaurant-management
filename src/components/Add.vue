<template>
  <Header />
  <h1>Hello User, Welcome to Add Restaurant Page</h1>
  <form class="add" @submit.prevent="addRestaurant">
    <input
      type="text"
      name="name"
      placeholder="Enter Name"
      v-model="restaurant.name"
    />
    <input
      type="text"
      name="address"
      placeholder="Enter Address"
      v-model="restaurant.address"
    />
    <input
      type="text"
      name="contact"
      placeholder="Enter Contact"
      v-model="restaurant.contact"
    />
    <button>Add new Restaurant</button>
  </form>
</template>

<script>
import axios from "axios";
import Header from "./Header";

export default {
  name: "Add",
  components: { Header },
  data() {
    return {
      restaurant: {
        name: "",
        address: "",
        contact: "",
      },
    };
  },
  methods: {
    async addRestaurant() {
      const result = await axios.post("http://localhost:3000/restaurant", {
        name: this.restaurant.name,
        address: this.restaurant.address,
        contact: this.restaurant.contact,
      });
      if (result.status === 201) {
        this.$router.push({ name: "Home" });
      }
    },
  },
  mounted() {
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "Login" });
    } else {
    }
  },
};
</script>

<style>
</style>