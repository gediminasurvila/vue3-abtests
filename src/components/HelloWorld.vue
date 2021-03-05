<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <a-button v-if="variant === 1" :buttonText="buttonText" />
    <b-button v-if="variant === 2" :buttonText="buttonText" />
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
        const variant = window.google_optimize.get("vVqcR17oSl2Kkr5ghRCJ5A");
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
        case 1:
          return "Click me";

        case 2:
          return "Click here";

        default:
          return "Original"
      }
    },
  },
  methods: {
    setVariant(variant) {
      this.variant = variant;
    }
  },
};
</script>
