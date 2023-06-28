<template lang="">
  <div>
    <img />
    <p>naam</p>
    <p>Prijs</p>
    <p>timer</p>
    <p>{{ currentLetter }}</p>
  </div>
</template>
<script>
export default {
  data() {
    return {
      assortment: {
        A: {
          naam: "Name A",
        },
        B: {
          naam: "Name B",
        },
        C: {
          naam: "Name C",
        },
        D: {
          naam: "Name C",
        },
        G: {
          naam: "Name C",
        },
        H: {
          naam: "Name C",
        },
        I: {
          naam: "Name C",
        },
        J: {
          naam: "Name C",
        },
        K: {
          naam: "Name C",
        },
        L: {
          naam: "Name C",
        },
        M: {
          naam: "Name C",
        },
        O: {
          naam: "Name C",
        },
        R: {
          naam: "Name C",
        },
        S: {
          naam: "Name C",
        },
        T: {
          naam: "Name C",
        },
        V: {
          naam: "Name C",
        },
        W: {
          naam: "Name C",
        },
        Z: {
          naam: "Name C",
        },
      },
    };
  },
  props: {
    currentLetter: {
      type: String,
      required: true,
    },
  },
};
</script>
<style lang="scss"></style>
