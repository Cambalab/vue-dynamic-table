<template lang="html">
  <div class="flex-row-container">
    <div v-for="column in this.columns" :key="column.name" class="flex-container flex-wrap">
      <div v-if="column.type === 'select'" class="flex-container">
        <Select
          :optionsList="column.optionsList"
          :placeholder="column.placeholder"
          :selected="currentRow[column.name]"
          :index="index"
          :data="getData(column.name)"
          v-on:selectOption="setSelectedOption($event)">
        </Select>
      </div>
        <div v-if="column.type === 'textInput'" class="flex-container">
          <TextInput
            :type="column.inputType"
            :placeholder="column.placeholder"
            :disabled="column.disabled"
            :index="index"
            :textValue="currentRow[column.name]"
            :data="getData(column.name)"
            v-on:newTextInputValue="setTextInputValue($event)">
        </TextInput>
      </div>
      <div v-if="column.type === 'checkbox'" v-for="(label, idxCheck) in column.labelTexts" :key="idxCheck" class="flex-wrap">
        <Checkbox
          :type="column.checkboxType"
          :text="label"
          :checked="currentRow[column.name]"
          :index="idxCheck"
          :data="getData(column.name)"
          v-on:newCheckboxValue="setCheckboxValue({data: $event, column: column.name, idxCheck: idxCheck})">
        </Checkbox>
      </div>
    </div>
  </div>
</template>

<script>
import Select from './Select.vue'
import Checkbox from './Checkbox.vue'
import TextInput from './TextInput.vue'

export default {
  name: 'Row',
  props: {
    columns: {
      type: Array,
      required: true
    },
    rows: {
      type: Array,
      required: true
    },
    currentRow: {
      type: Object,
      required: true
    },
    index: {
      type: Number,
      required: true
    },
    data: {
      type: Object,
      required: false
    }
  },
  components: {
    Select,
    Checkbox,
    TextInput
  },
  computed: {
  },
  methods: {
    setSelectedOption (option) {
      let column = Object.keys(this.currentRow)[0]
      this.currentRow[column] = option.selectedOption
      this.$emit('selectedOption', {column: column, value: option.selectedOption})
    },
    setTextInputValue (stringValue) {
      let column = Object.keys(this.currentRow)[stringValue.index]
      console.log(Object.keys(this.currentRow))
      console.log(column)
      this.$emit('textInputValue', {column: column, value: stringValue.textInputValue})
    },
    getData (column) {
      if (this.data !== undefined) {
        if (this.data.length !== 0) {
          return this.data[column]
        } else {
          return null
        }
      }
    }
  },
  created () {
    // console.log(`DATA EN ROW: ${JSON.stringify(this.data)}`)
  }
}
</script>

<style lang="css">
</style>
