<template>
  <div>
    <h1>Détail</h1>
    <div class="title">{{ house.attributes.titre }}</div>
  </div>
</template>

<script>
export default {
  name: "DetailHouse",
  props: ["id"],
  data() {
    return {
      house: {},
      headers: {
        "Content-Type": "application/json",
      },
    };
  },
  methods: {
    parseJSON: function (resp) {
      return resp.json ? resp.json() : resp;
    },
    checkStatus: function (resp) {
      if (resp.status >= 200 && resp.status < 300) {
        return resp;
      }
      return this.parseJSON(resp).then((resp) => {
        throw resp;
      });
    },
  },
  async mounted() {
    try {
      const response = await fetch(
        `http://localhost:1337/api/houses/${this.$route.params.id}`,
        {
          method: "GET",
          headers: this.headers,
        }
      )
        .then(this.checkStatus)
        .then(this.parseJSON);
      this.house = response.data;
      console.log(this.house.data);
    } catch (error) {
      this.error = error;
    }
  },
};
</script>

<style>
</style>