<template lang="html">
  <div class="flex-container flex-wrap">
    <div class="flex-row-container box" id="one">
      <DynamicTable
        :columns="this.columnsForTableOne()"
        :rows="this.rowsForTableOne"
        :data="this.dataForTableOne"
        v-on:addRow="addRow('one')"
        v-on:selectedOption="setSelectedOption($event)"
        v-on:deleteRow="deleteRow($event, 'one')">
      </DynamicTable>
    </div>
    <div class="flex-row-container box" id="two">
      <DynamicTable
        :columns="this.columnsForTableTwo()"
        :rows="this.rowsForTableTwo"
        :data="this.dataForTableTwo"
        v-on:addRow="addRow('two')"
        v-on:textInputValue="setTextInputValue($event)"
        v-on:deleteRow="deleteRow($event, 'two')">
      </DynamicTable>
    </div>
    <div class="flex-row-container box" id="three">
      <DynamicTable
        :columns="this.columnsForTableThree()"
        :rows="this.rowsForTableThree"
        :data="this.dataForTableThree"
        v-on:addRow="addRow('three')">
      </DynamicTable>
    </div>
    <div class="flex-row-container box" id="four">
      <DynamicTable
        :columns="this.columnsForTableFour()"
        :rows="this.rowsForTableFour"
        :data="this.dataForTableFour"
        v-on:addRow="addRow('four')"
        v-on:selectedOption="setSelectedOption($event)"
        v-on:deleteRow="deleteRow($event, 'four')">
      </DynamicTable>
    </div>
    <div class="flex-row-container box" id="five">
      <DynamicTable
        :columns="this.columnsForTableFive()"
        :rows="this.rowsForTableFive"
        :data="this.dataForTableFive"
        v-on:addRow="addRow('five')"
        v-on:selectedOption="setTextInputValue($event)"
        v-on:deleteRow="deleteRow($event, 'five')">
      </DynamicTable>
    </div>
  </div>
</template>
<script>
import DynamicTable from './DynamicTable.vue'
import {
  OPTIONS_LIST,
  DATA_FOR_TABLE_ONE,
  DATA_FOR_TABLE_TWO,
  DATA_FOR_TABLE_THREE,
  DATA_FOR_TABLE_FOUR,
  DATA_FOR_TABLE_FIVE
  } from '@/store/FakeData.js'

export default {
  name: 'HomeView',
  data () {
    return {
      rowsForTableOne: [],
      rowsForTableTwo: [],
      rowsForTableThree: [],
      rowsForTableFour: [],
      rowsForTableFive: [],
      objectDataTalbeOne: {
        select_column: []
      },
      objectDataTalbeTwo: {
        textInput_column: null,
        textInput_number_column: null,
        textInput_disable_column: null
      }
    }
  },
  components: {
    DynamicTable
  },
  computed: {
    optionsListForTable: function () {
      return OPTIONS_LIST
    },
    dataForTableOne: function () {
      return DATA_FOR_TABLE_ONE
    },
    dataForTableTwo: function () {
      return DATA_FOR_TABLE_TWO
    },
    dataForTableThree: function () {
      return DATA_FOR_TABLE_THREE
    },
    dataForTableFour: function () {
      return DATA_FOR_TABLE_FOUR
    },
    dataForTableFive: function () {
      return DATA_FOR_TABLE_FIVE
    }
  },
  methods: {
    columnsForTableOne () {
      return [
        {name: 'select_column', type: 'select', placeholder: 'Select an option for this column', optionsList: this.optionsListForTable}
      ]
    },
    columnsForTableTwo () {
      return [
        {name: 'textInput_column', type: 'textInput', placeholder: 'Write here', inputType: 'text'},
        {name: 'textInput_number_column', type: 'textInput', placeholder: 'Enter only numbers', inputType: 'number'},
        {name: 'textInput_disabled_column', type: 'textInput', placeholder: 'I am a disabled input', disabled: true, inputType: 'text'}
      ]
    },
    columnsForTableThree () {
      return [
        {name: 'checkbox_column', type: 'checkbox', labelTexts: ['One', 'Two', 'Three']},
        {name: 'checkbox_radio_column', type: 'checkbox', labelTexts: ['One', 'Two', 'Three'], checkboxType: 'radio'}
      ]
    },
    columnsForTableFour () {
      return [
        {name: 'select_column', type: 'select', placeholder: 'Select an option for this column', optionsList: this.optionsListForTable}
      ]
    },
    columnsForTableFive () {
      return [
        {name: 'textInput_column', type: 'textInput', placeholder: 'Write here', inputType: 'text'},
        {name: 'textInput_number_column', type: 'textInput', placeholder: 'Enter only numbers', inputType: 'number'},
        {name: 'textInput_disabled_column', type: 'textInput', placeholder: 'I am a disabled input', disabled: true, inputType: 'text'}
      ]
    },
    addRow (table) {
      switch (table) {
        case 'one':
          this.rowsForTableOne.push({
            select_column: null
          })
          break
        case 'two':
          this.rowsForTableTwo.push({
            textInput_column: null,
            textInput_number_column: null,
            textInput_disable_column: null
          })
          break
        case 'three':
          this.rowsForTableThree.push({
            checkbox_column: null,
            checkbox_radio_column: null
          })
          break
        case 'four':
          this.rowsForTableFour.push({
            select_column: null
          })
          break
        case 'five':
          this.rowsForTableFive.push({
            textInput_column: null,
            textInput_number_column: null,
            textInput_disable_column: null
          })
          break
        default:
      }
    },
    deleteRow (rowIndex, table) {
    },
    setSelectedOption (option) {
      this.objectDataTalbeOne[option.column].push(option.value)
    },
    setTextInputValue (value) {
      this.objectDataTalbeTwo[value.column] = value.value
    },
    initTables () {
      DATA_FOR_TABLE_FOUR.forEach(row => {
        this.rowsForTableFour.push(row)
      })
      DATA_FOR_TABLE_FIVE.forEach(row => {
        this.rowsForTableFive.push(row)
      })
    }
  },
  created () {
    let tables = ['one', 'two', 'three']
    tables.forEach(table => this.addRow(table))
    this.initTables()
  }
}
</script>
<style scoped>
  .box {
    width: 30%;
    margin: 5px 20px 5px 20px;
  }

  .flex-wrap {
    flex-wrap: wrap;
  }
</style>
