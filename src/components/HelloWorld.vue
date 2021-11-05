<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <a-button v-if="variant === '0'" :buttonText="buttonText" />
    <b-button v-if="variant === '1'" :buttonText="buttonText" />
  </div>
</template>

<script>
import AButton from "../components/abtests/AButton";
import BButton from "../components/abtests/BButton";

export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  components: {
    AButton,
    BButton,
  },
  async created() {
    if (window.dataLayer) {
      await window.dataLayer.push({ event: "optimize.activate" });
    }
    this.intervalId = setInterval(() => {
      if (window.google_optimize !== undefined) {
        const variant = window.google_optimize.get("xpkYuNrOSWKfsXLo6OB4cw");
        console.log("variant", variant);
        this.setVariant(variant);
        clearInterval(this.intervalId);
      }
    }, 100);
  },
  data() {
    return {
      variant: null,
    };
  },
  computed: {
    buttonText() {
      switch (this.variant) {
        case '0':
          return "Click me";

        case '1':
          return "Click here";
      }
    },
  },
  methods: {
    setVariant(variant) {
      console.log("Setting variant", variant);
      this.variant = variant;
    }
  },
};
</script>
