# My Vue Modal
A simple Modal component for Vue.

## How to use
Download the component file and place it in your `components/` folder.  
Then, you can import it with `import Modal from "@/components/Modal.vue";`.  
Then simply call it with `<Modal>Your content</Modal>`.

## Content
You can put any HTML code you wish between the opening and ending tags.  
You can pass two optionnal parameters to the component :
- `displayed`, a boolean that defaults to `false` and tells whether the modal should be displayed or not as the page loads
- `btnClose`, a boolean that defaults to `true` and tells whether a close button should be displayed or not at the top-right corner of the overlay.

## Event
This component fires a `close` event when the close button is triggered, the Escape key pressed or when the user clicks outside of the modal. You can watch for it in order to put the `displayed` prop to false to close the modal.

## Usage example
```html
<Modal :displayed="isModalDisplayed" @close="isModalDisplayed = false">
  <p>Look at that beautiful modal! =D</p>
</Modal>

<script>
  import Modal from "@/components/Modal.vue";
  
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
