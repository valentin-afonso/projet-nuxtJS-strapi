<template>
  <div id="app">
    <h1>Houses</h1>
    <div v-if="error">
      {{ error }}
    </div>
    <div v-else class="container-list">
      <!--  <div class="title">{{ house.attributes.titre }}</div>
        <a v-on:click="$emit()">Detail</a> -->

      <nuxt-link
        :to="`/liste/` + house.id"
        v-for="house in houses"
        :key="house.id"
      >
        <TeaserHouse
          :titre="house.attributes.titre"
          :prix="house.attributes.prix"
          class="house"
        />
      </nuxt-link>
    </div>
    <!--
    <img :src="http://localhost:1337/api/upload/files/{}" alt="" />
    http://localhost:1337/uploads/mainson2_b5c5ced619.jfif?updated_at=2022-03-17T16:36:35.897Z
    -->
  </div>
</template>

<script>
import TeaserHouse from "~/components/TeaserHouse";
export default {
  components: {
    TeaserHouse,
  },
  name: "Houses",
  data() {
    return {
      houses: [],
      error: null,
      headers: {
        "Content-Type": "application/json",
      },
    };
  },
  /*
  computed: {
    changed_post_content: function () {
      return post_content
        .split("/uploads/")
        .join(`http://localhost:1337/api/upload/files`);
    },
  },
  */
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
      const response = await fetch("http://localhost:1337/api/houses", {
        method: "GET",
        headers: this.headers,
      })
        .then(this.checkStatus)
        .then(this.parseJSON);
      this.houses = response.data;
      console.log(this.houses.data);
    } catch (error) {
      this.error = error;
    }
  },
};
</script>

<style>
.container-list {
  display: flex;
}
.container-list .house {
  margin: 1rem;
}
</style>