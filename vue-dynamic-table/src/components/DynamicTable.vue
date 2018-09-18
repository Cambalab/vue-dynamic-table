<template lang="html">
  <div class="">
    <tableHeader
      :columnsHeader="this.columns"
      :showAddRowButton="this.showAddRowButton">
    </tableHeader>
    <div v-for="column in this.columns">
      <div v-if="column.type === 'select'">
        <select
          :optionsList="column.optionsList"
          :placeholder="column.placeholder"
          :selected="currentElement[column.name]"
          :index="index"
          :data=""
          v-on:selectOption="setSelectedOption($event)">
        </select>
      </div>
      <div v-if="column.type === 'textInput'">
        <textInput
          :type="column.inputType"
          :placeholder="column.placeholder"
          :disabled="column.disabled"
          :index="index"
          :textValue="currentElement[column.name]"
          :data=""
          v-on:newTextInputValue="setTextInputValue($event)">
        </textInput>
      </div>
    </div>
  </div>
</template>

<script>

import Select from './Select.vue'
import Checkbox from './Checkbox.vue'
import TextInput from './TextInput.vue'
import TableHeader from './TableHeader.vue'
import DeleteRowButton from './DeleteRowButton.vue'

export default {
  props: {
    columns: {
      type: Array,
      required: true
    },
    rows: {
      type: Array,
      required: true
    },
    currentElement: {
      type: Object,
      required: true
    },
    index: {
      type: Number,
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
      type: Object,
      required: false,
      default: {}
    }
  },
  components: {
    Select,
    Checkbox,
    TextInput,
    TableHeader,
    DeleteRowButton
  },
  computed: {
  },
  methods: {
  },
  watch: {
  },
  create() {
  }
}
</script>

<style lang="css">
</style>
