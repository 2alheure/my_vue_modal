# Vue.js Modal
A simple Modal component for Vue.js.

- [Vue.js Modal](#vuejs-modal)
  - [Installation](#installation)
  - [Usage](#usage)
    - [Simple usage example](#simple-usage-example)
    - [Props](#props)
    - [Events](#events)

## Installation
First, run `npm install @2alheure/vue-modal`.  
Then import it with `import Modal from "@2alheure/vue-modal";`.  

## Usage
### Simple usage example
```html
<Modal :displayed="isModalDisplayed" @close="isModalDisplayed = false">
  <p>Look at that beautiful modal! =D</p>
</Modal>

<!-- OR -->

<Modal v-model="isModalDisplayed">
  <p>Look at that beautiful modal! =D</p>
</Modal>



<script>
  import Modal from "@2alheure/vue-modal";
  
  export default {
    components: {
      Modal
    },
    data() {
      isModalDisplayed: true
    }
  }
</script>
```

### Props
| Name         |  Type   | Default value | Description                                                                                                                                |
| :----------- | :-----: | :-----------: | ------------------------------------------------------------------------------------------------------------------------------------------ |
| displayed    | Boolean |    `false`    | Whether the modal should be displayed or not. <br><br>This is the prop actually used by the `v-model` directive.<br>This prop is required. |
| adaptative   | Boolean |    `false`    | Whether to let the modal adapt its size to its content or not. If not, the modal will be half the width of the window.                     |
| btnClose     | Boolean |    `true`     | Whether a "close" button should be displayed or not.                                                                                       |
| escClose     | Boolean |    `true`     | Whether the modal should close when the "escape" key is pressed or not.                                                                    |
| overlayClose | Boolean |    `true`     | Whether the modal should close when the user clicks outside its content or not.                                                            |

### Events
| Name  | Value type |  Value  | Description                                                                                                                                                                                                  |
| :---- | :--------: | :-----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| close |  Boolean   | `false` | Triggered each time the modal *should be* closed: <br>The cross button or the outside of the modal has been cliked, escape key has been pressed. <br><br>This is the event used for the `v-model` directive. |
| open  |  Boolean   | `true`  | Triggered each time the modal is opened.                                                                                                                                                                     |

