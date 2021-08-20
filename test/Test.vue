<template>
  <main>
    <Modal v-model="isModalDisplayed">
      <p>Look at that beautiful modal! =D</p>
    </Modal>

    <button @click="isModalDisplayed = true">Click me to open the modal</button>
  </main>
</template>



<script>
  import Modal from "../src/Modal.vue";

  export default {
    components: {
      Modal
    },
    data() {
      return {
        isModalDisplayed: false
      };
    }
  }
</script>