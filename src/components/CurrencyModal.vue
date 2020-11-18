<template>
  <Modal @close="closeWindow">
    <template #body>
      <label>
        USD
        <input type="text" v-model="inputUsd">
      </label>
      <label>
        RUB
        <input type="text" v-model="inputRub">
      </label>
      <label>
        UAH
        <input type="text" v-model="inputUah">
      </label>
    </template>
    <template #footer>
      <button @click="saveData">Save</button>
      <button @click="closeWindow">Cancel</button>
    </template> 
  </Modal>
</template>


<script>
import Modal from './Modal';

export default {
  props: {
    clickedItem: {
      type: Object,
      required: true
    }
  },
  
  components: {
    Modal,
  },

  data() {
    return {
      items: JSON.parse(localStorage.getItem('items')) ? JSON.parse(localStorage.getItem('items')) : [],
      inputUsd: this.clickedItem.usd,
      inputRub: this.clickedItem.rub,
      inputUah: this.clickedItem.uah
    }
  },
  methods: {
    saveData(event) {   
      if (this.clickedItem) {
        let item = Object.values(this.items).find(elem => elem.Id === this.clickedItem.Id);
        item.usd = this.inputUsd;
        item.rub = this.inputRub;
        item.uah = this.inputUah;
        const newList = Object.values(this.items).map(o => {
          if (o.Id === item.Id) {
            return item;
          }
          return o;
        });
        localStorage.setItem('items', JSON.stringify(newList))
        this.$emit('data-update-clicked-item')
        this.$emit('data-update')
      } else {
        let newItem = {
          usd: this.inputUsd,
          rub: this.inputRub,
          uah: this.inputUah,
          Id: this.items.length
        }
        this.items.push(newItem);
        localStorage.setItem('items', JSON.stringify(this.items))
        this.$emit('data-update')
      }

      this.closeWindow();
    },

    closeWindow() {
      this.$emit('close-modal')
    },
  },
};
</script>