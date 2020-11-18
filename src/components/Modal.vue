<template>
  <div class="modal-overlay">
    <div class="modal-window">
      <div class="modal-header">
        <span class="modal-title"></span>
        <span
          class="modal-close"
          @click="$emit('close')"
        >&times;</span>
      </div>
      <div class="modal-body">
        <slot name="body"/>
      </div>
      <div class="modal-footer">
        <slot name="footer" />
      </div>
    </div>
  </div>
</template>


<script>
export default {
  name: 'Modal',
}
</script>

<style scoped>

.modal-window {
  width: 600px;
  border-radius: 5px;
  background-color:rgba(0, 0, 0, .5);
  margin: 0  auto;
}

.modal-header {
  padding: 5px 10px;
  display: flex;
  justify-content: space-between;
  border-bottom: 1px solid #eee;
}

.modal-title {
  font-size: 1.5rem;
}

.modal-body p {
  margin: 0 0 5px;
}

.modal-body {
  padding: 10px;
  display: flex;
  justify-content: space-between;
}

.modal-footer {
  padding: 5px 10px;
  border-top: 1px solid #eee;
}

input {
  max-width: 120px;
}

.modal-overlay {
  position: fixed;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
}
</style>