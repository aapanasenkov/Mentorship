<template>
  <div class="app">
    <button @click="toggleWindow">Add</button>
    <table>
      <tr>
        <th>USD</th>
        <th>RUB</th>
        <th>UAH</th>
        <th>Actions</th>
      </tr>
      <ItemsList
        @clickedItem="getClickedItem"
        @close-modal="toggleWindow"
        :items="items"
      />
    </table>
    <div class="modalWindow">
      <CurrencyModal
        :clickedItem="clickedItem"
        v-if="open"
        @close-modal="toggleWindow"
        @data-update="updateDate"
        @data-update-clicked-item="getClickedItem"
      />
    </div>
  </div>
</template>

<script>
import ItemsList from '@/components/ItemsList'
import CurrencyModal from '@/components/CurrencyModal'
export default {
  name: 'App',
  data() {
    return {
      items: JSON.parse(localStorage.getItem('items') || '[]'),
      open: false,
      clickedItem: ''
    }
  },

  methods: {
    addItem(event) {
      let newItem = {
        usd: '1',
        rub: '2',
        uah: '3'
      }
      this.items.push(newItem);
      localStorage.setItem('items', JSON.stringify(this.items))
    },

    toggleWindow() {
      this.open = !this.open;
      this.clickedItem = ''
    },

    updateDate() {
      this.items = JSON.parse(localStorage.getItem('items')) ? JSON.parse(localStorage.getItem('items')) : []
    },

    getClickedItem(value) {
      this.clickedItem = this.clickedItem ? '' : value
    }
  },

  components: {
    ItemsList,
    CurrencyModal,
  }
}
</script>

<style>

table, th, td {
  border: 1px solid black;
}

</style>
