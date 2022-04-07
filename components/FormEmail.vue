<template>
  <form @submit.prevent="handle">
    <LabelAndInput labelName="email" type="email" v-model="email" />
    <LabelAndInput labelName="message" type="text" />
    <LabelAndInput type="submit" />
  </form>
</template>

<script>
export default {
  name: "NuxtTutorial",
  data() {
    return { email: "" };
  },
  methods: {
    handle() {
      console.log(this.email);
      fetch("https://formspree.io/f/mayvjgqn", {
        method: "POST",
        body: JSON.stringify({ email: this.email }),
        headers: {
          Accept: "application/json",
        },
      });
    },
  },
};
</script>
