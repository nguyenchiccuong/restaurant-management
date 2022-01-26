<template>
  <Header />
  <h1>Hello User, Welcome to Update Restaurant Page</h1>
  <form class="add" @submit.prevent="updateRestaurant">
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
    <button>Update Restaurant</button>
  </form>
</template>

<script>
import Header from "./Header";
import axios from "axios";

export default {
  name: "Update",
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
    async updateRestaurant() {
      const result = await axios.put(
        `http://localhost:3000/restaurant/${this.$route.params.id}`,
        {
          name: this.restaurant.name,
          address: this.restaurant.address,
          contact: this.restaurant.contact,
        }
      );
      if (result.status === 200) {
        this.$router.push({ name: "Home" });
      }
    },
  },
  async mounted() {
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "Login" });
    } else {
      const result = await axios.get(
        `http://localhost:3000/restaurant/${this.$route.params.id}`
      );
      this.restaurant.name = result.data.name;
      this.restaurant.address = result.data.address;
      this.restaurant.contact = result.data.contact;
    }
  },
};
</script>

<style>
</style>