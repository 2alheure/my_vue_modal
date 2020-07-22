<style lang="postcss" scoped>
.modal {
  background-color: rgba(40, 40, 40, 0.75);
  transition: opacity 0.25s ease;

  position: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  overflow-y: auto;
}

.modal.displayed {
  cursor: pointer;
}

.modal.not-displayed {
  opacity: 0;
  pointer-events: none;
}

.modal p.btn-close {
  position: absolute;
  top: 0;
  right: 0;
  margin: 0.25rem 1rem;
  cursor: pointer;
  font-size: 1.5rem;
  color: #a0aec0;
}

.modal > div.adaptative {
  display: inline-block;
}

.modal > div {
  max-width: 80%;
  margin: 10vh auto;
  padding: 2rem 1rem;
  background-color: #fff;
  border-radius: 0.25rem;
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1),
    0 4px 6px -2px rgba(0, 0, 0, 0.05);
  cursor: default;
}
</style>

<template>
  <div :class="['modal', displayed? 'displayed' : 'not-displayed']" @click.self="close">
    <p v-if="btnClose" class="btn-close" @click="close">&times;</p>
    <div :class="adaptative ? 'adaptative' : 'not-adaptative'">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "modal",
  props: {
    displayed: Boolean,
    adaptative: Boolean,
    btnClose: {
      type: Boolean,
      default: true
    }
  },
  methods: {
    close() {
      this.$emit("close");
    },
    handleEscClose(e) {
      if (e.keyCode == 27) this.close();
    }
  },
  mounted() {
    if (this.displayed) {
      document.body.classList.add("overflow-hidden");
      document.addEventListener("keydown", this.handleEscClose);
    } else document.body.classList.remove("overflow-hidden");
  },
  watch: {
    displayed: function(n) {
      if (n) {
        document.body.classList.add("overflow-hidden");
        document.addEventListener("keydown", this.handleEscClose);
      } else {
        document.body.classList.remove("overflow-hidden");
        document.removeEventListener("keydown", this.handleEscClose);
      }
    }
  }
};
</script>
