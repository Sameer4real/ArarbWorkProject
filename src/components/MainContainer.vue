<template>
  <b-container fluid>
    <b-row align-v="streach">
      <b-col cols="4" class="card-container">
        <h1 class="title">ArabWork Project</h1>
        <UserCard
          v-for="(user, x) in usersData"
          :key="x"
          v-bind:user="user"
          @changeCord="ChangeCord($event)"
        />
        <div class="pagenation">
          <b-button
            size="lg"
            variant="outline-primary"
            class="pagenation-btn"
            @click="previusUsers"
            >Previous</b-button
          >
          <b-button
            size="lg"
            variant="primary"
            class="pagenation-btn"
            @click="nextUsers"
            >Next</b-button
          >
        </div>
      </b-col>
      <b-col cols="8" class="map-container">
        <iframe
          width="100%"
          height="100vh"
          class="map"
          :src="`https://www.google.com/maps/embed/v1/place?q=${lat},${long}&amp;key=AIzaSyD5ORdQ0kF6pM2ciBNuj1h_6KQIe7VPHiE`"
        ></iframe>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import axios from "axios";
import UserCard from "./UserCard.vue";

export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  components: {
    UserCard,
  },
  data() {
    return {
      usersData: [],
      currentPage: 1,
      long: 135.6354,
      lat: 89.4367,
    };
  },
  methods: {
    async created(currentPage) {
      try {
        const response = await axios.get(
          `https://randomuser.me/api/?page=${currentPage}&results=5&seed=abc&inc=name,gender,email,location,dob,picture`
        );
        this.usersData = response.data.results;
      } catch (error) {
        console.error(error);
      }
    },
    nextUsers() {
      this.created(this.currentPage + 1);
      this.currentPage = this.currentPage + 1;
    },
    previusUsers() {
      this.created(this.currentPage - 1);
      this.currentPage = this.currentPage - 1;
    },
    ChangeCord(newCord) {
      this.long = newCord.longitude;
      this.lat = newCord.latitude;
    },
  },
  mounted() {
    this.created();
  },
};
</script>

<style scoped>
.main-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.card-container {
  display: flex;
  flex-direction: column;
  gap: 30px;
  justify-content: space-between;
  margin-top: -50px;
}

.title {
  text-align: center;
  margin-top: 20px;
  font-weight: 700;
  font-size: 40px;
  color: #333;
}

.pagenation {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
  margin-bottom: 20px;
}

.pagenation-btn {
  width: 160px;
}

.map {
  width: 100%;
  height: 100%;
}
.map-container {
  height: 100vh;
  position: fixed;
  top: 20;
  bottom: 0;
  right: 0;
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
