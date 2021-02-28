<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <button>{{ buttonText }}</button>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  async created() {
    if (window.dataLayer) {
      await window.dataLayer.push({ event: "optimize.activate" });
    }
    this.intervalId = setInterval(() => {
      if (window.google_optimize !== undefined) {
        const variant = window.google_optimize.get("vVqcR17oSl2Kkr5ghRCJ5A");
        console.log("variant", variant);
        clearInterval(this.intervalId);
      }
    }, 100);
  },
  data() {
    return {
      buttonText: "Click Me",
    };
  },
};
</script>
