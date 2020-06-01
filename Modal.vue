<style lang="postcss" scoped>
.modal {
  background-color: rgba(40, 40, 40, .75);
  transition: opacity 0.25s ease;
}

.modal div {
  margin: 10vh auto;
  max-width: 80%;
}
</style>

<template>
  <div
    :class="['modal', displayed? 'cursor-pointer' : 'opacity-0 pointer-events-none', 'fixed top-0 left-0 bottom-0 right-0 overflow-y-auto']"
      @click="close"
      @keydown.esc="close"
  >
    <div
      class="py-8 px-4 bg-white rounded shadow-lg flex justify-center"
    >
      <p
        v-if="btnClose"
        class="absolute top-0 right-0 text-2xl my-1 mx-4 cursor-pointer text-gray-500"
        @click="close"
      >&times;</p>
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "modal",
  props: {
    displayed: Boolean,
    btnClose: {
      type: Boolean,
      default: true
    }
  },
  methods: {
    close() {
      this.$emit("close");
    }
  },
  mounted() {
    if (this.displayed) document.body.classList.add('overflow-hidden');
    else document.body.classList.remove('overflow-hidden');
  },
  updated() {
    if (this.displayed) document.body.classList.add('overflow-hidden');
    else document.body.classList.remove('overflow-hidden');
  }
};
</script>