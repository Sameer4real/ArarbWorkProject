<template>
  <div>
    <b-card no-body class="overflow-hidden shadow-box">
      <b-row no-gutters>
        <b-col md="6">
          <b-card-img
            :src="user.picture.medium"
            alt="Image"
            class="rounded-0"
          ></b-card-img>
        </b-col>
        <b-col md="6">
          <b-card-body
            :title="`${user.name.title} ${user.name.first} ${user.name.last}`"
          >
            <b-card-text class="text-style">{{ user?.email }}</b-card-text>
            <b-card-text class="text-style">{{ user?.gender }}</b-card-text>
            <b-card-text class="text-style">{{
              user?.location?.country
            }}</b-card-text>
            <b-card-text class="text-style">{{
              user?.dob?.date?.substring(0, 10)
            }}</b-card-text>

            <b-button size="lg" variant="primary" @click="passEvent"
              >View location on maps</b-button
            >
          </b-card-body>
        </b-col>
      </b-row>
    </b-card>
  </div>
</template>

<script>
export default {
  name: "UserCard",
  props: {
    user: {
      type: Object,
      default: () => ({}),
    },
  },
  data() {
    return {
      fullName:
        this.user.name.title +
        " " +
        this.user.name.first +
        " " +
        this.user.name.last,
    };
  },
  methods: {
    passEvent() {
      console.log("what it do", this.user.location.coordinates.latitude);
      this.$emit("changeCord", this.user?.location?.coordinates);
    },
  },
  mounted: function () {
    console.log(this.user, "user");
  },
};
</script>

<style scoped>
.card-body {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-top: 20px;
  justify-content: center;
}

.text-style {
  font-size: 1.2rem;
  color: #333;
}

.shadow-box {
  box-shadow: 10px 10px 25px -7px rgba(0, 0, 0, 0.2);
}
</style>
