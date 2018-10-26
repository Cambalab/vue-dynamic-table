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
          v-on:selectOption="setSelectedOption($event, column.name)">
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
            v-on:newTextInputValue="setTextInputValue($event, column.name)">
        </TextInput>
      </div>
      <div v-if="column.type === 'checkbox'" v-for="(label, idxCheck) in column.labelTexts" :key="idxCheck" class="flex-wrap">
        <Checkbox
          :type="column.checkboxType"
          :text="label"
          :checked="currentRow[column.name]"
          :index="idxCheck"
          :data="getData(column.name)"
          v-on:newCheckboxValue="setCheckboxValue($event, column.name, idxCheck)">
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
    setSelectedOption (option, column) {
      this.currentRow[column] = option.selectedOption
      this.$emit('selectedOption', {column: column, value: option.selectedOption})
    },
    setTextInputValue (stringValue, column) {
      this.currentRow[column] = stringValue.textInputValue
      this.$emit('textInputValue', {column: column, value: stringValue.textInputValue})
    },
    setCheckboxValue (option, column, checkboxIndex) {
      console.log(option)
      console.log(checkboxIndex)
      if (option.checkboxValue) {
        this.currentRow[column][checkboxIndex] = {idxCheck: option.idxCheck, value: option.checkboxValue}
      } else {
        let idx = this.currentRow[column].findIndex(check => check.idxCheck === option.idxCheck)
        this.currentRow[column].splice(idx, 1)
      }
      this.$emit('checkboxValue', {column: column, value: option.checkboxValue, idxCheck: checkboxIndex})
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
  }
}
</script>

<style lang="css">
</style>
