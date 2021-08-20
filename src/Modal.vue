<style lang="postcss" scoped>
  .modal {
    background-color: rgba(40, 40, 40, 0.75);
    transition: opacity 0.25s ease;

    position: fixed;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;

    overflow: auto;

    display: flex;
    flex-direction: column;
    align-items: center;
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

  .modal>div.adaptative {
    max-width: 90%;
    min-width: 1rem;
  }

  .modal>div.not-adaptative {
    width: 50%;
  }

  .modal>div {
    margin: 5vh auto;
    padding: 2rem 1rem;
    background-color: #fff;
    border-radius: 0.25rem;
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1),
      0 4px 6px -2px rgba(0, 0, 0, 0.05);
    cursor: default;
    position: relative;
  }

  .cursor-pointer {
    cursor: pointer;
  }

  .overflow-hidden {
    overflow: hidden;
  }
</style>

<template>
  <div :class="[
      'modal',
      modelValue ? 'displayed' : 'not-displayed',
      overlayClose ? 'cursor-pointer' : '',
    ]" @click.self="closeByOverlay">
    <div :class="adaptative ? 'adaptative' : 'not-adaptative'">
      <p v-if="btnClose" class="btn-close" @click="close">&times;</p>
      <slot></slot>
    </div>
  </div>
</template>

<script>
  export default {
    name: "modal",
    model: {
      event: "update:modelValue",
      prop: "modelValue",
    },
    props: {
      modelValue: Boolean,
      adaptative: Boolean,
      btnClose: {
        type: Boolean,
        default: true,
      },
      escClose: {
        type: Boolean,
        default: true,
      },
      overlayClose: {
        type: Boolean,
        default: true,
      },
    },
    methods: {
      close() {
        this.$emit("update:modelValue", false);
      },
      handleEscClose(e) {
        if (e.keyCode == 27) this.close();
      },
      closeByOverlay() {
        if (this.overlayClose) this.close();
      },
    },
    mounted() {
      if (this.modelValue) {
        document.body.classList.add("overflow-hidden");
        if (this.escClose)
          document.addEventListener("keydown", this.handleEscClose);
      } else document.body.classList.remove("overflow-hidden");
    },
    watch: {
      modelValue: function (n) {
        if (n) {
          document.body.style.overflow = "hidden";
          document.addEventListener("keydown", this.handleEscClose);
          this.$emit("open");
        } else {
          document.body.style.overflow = "inherit";
          if (this.escClose)
            document.removeEventListener("keydown", this.handleEscClose);
        }
      },
    },
  };
</script>