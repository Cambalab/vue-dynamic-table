<template lang="html">
  <div class="flex-container">
    <div class="flex-column-container">
      <TableHeader
        :columnsHeader="columns"
        :showAddRowButton="showAddRowButton"
        v-on:addNewRow="addRow()">
      </TableHeader>
      <div v-for="(currentRow, index) in this.rows" :key="index" class="flex-row-container">
        <Row
          :columns="columns"
          :rows="rows"
          :currentRow="currentRow"
          :index="index"
          :data="data[index]"
          class="tableRow"
          v-on:selectedOption="selectedOption($event)"
          v-on:textInputValue="textInputValue($event)"
          v-on:checkboxValue="checkboxValue($event)">
        </Row>
        <DeleteRowButton
          :showMinusButton="showDeleteRowButton"
          :index="index"
          v-on:deleteRow="deleteRow($event)">
        </DeleteRowButton>
      </div>
    </div>
  </div>
</template>

<script>
import Row from './Row.vue'
import TableHeader from './TableHeader.vue'
import DeleteRowButton from './DeleteRowButton.vue'

export default {
  name: 'DynamicTable',
  data () {
    return {
      value: false
    }
  },
  props: {
    columns: {
      type: Array,
      required: true
    },
    rows: {
      type: Array,
      required: true
    },
    showAddRowButton: {
      type: Boolean,
      required: false,
      default: true
    },
    showDeleteRowButton: {
      type: Boolean,
      required: false,
      default: true
    },
    data: {
      type: Array,
      required: false
    }
  },
  components: {
    Row,
    TableHeader,
    DeleteRowButton
  },
  computed: {
  },
  methods: {
    addRow () {
      this.$emit('addRow')
    },
    deleteRow (rowIndex) {
      this.rows.splice(rowIndex, 1)
      if (this.rows.length < 1) {
        this.addRow()
      }
      this.$emit('deleteRow', rowIndex)
    },
    selectedOption (option) {
      this.$emit('selectedOption', option)
    },
    textInputValue (value) {
      this.$emit('textInputValue', value)
    },
    checkboxValue (value) {
      this.$emit('checkboxValue', value)
    }
  },
  watch: {
  },
  created () {
  }
}
</script>

<style lang="css">
</style>
