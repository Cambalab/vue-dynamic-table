# Vue Dynamic Table

**Vue Dynamic Table** es un plugin para **Vue.js** con el que vas a poder crear tablas customizables y dinámicas para formularios.

#### Características
* Poder elegir la cantidad de columnas.
* Poder elegir el tipo de campo que va a tener cada columna.
* Poder elegir la cantidad de filas.
* Agregar y/o eliminar filas dinámicamente.
* Cambiar el tipo de icono de agregar y eliminar fila.
---
## Descarga e instalación de demo

``` bash
# clonar el repositorio
git clone https://github.com/LeonardoVaquel/vue-dynamic-table

# ir al directorio
cd vue-dynamic-table

# instalar dependencias
npm install

# levantar el server con hotreload en localhost:8080
npm run dev
```
---
## Modo de uso

* Importar Vue Dynamic Table
``` javascript
import DynamicTable from '/ubicacion_del_plugin'
```

* Declarar el Componente
``` javascript
components: {
  DynamicTable
},
```

* En el template usar el tag de ```<DynamicTable>```
``` html
<DynamicTable
  {props}
>
</DynamicTable>
```
---
## Props
* **columns** : Recibe un Array de objectos donde cada objeto es una columna. Es requerido para que se renderize la tabla.
``` javascript
columns: {
  type: Array,
  required: true
},
```
* **rows** : Recibe un Array donde van a estar cada fila de la tabla. Es requerido para que se renderize la tabla.
``` javascript
rows: {
  type: Array,
  required: true
},
```
* **showAddRowButton** : Recibe un Boolean indicando si se muestra el botón para agregar filas. No es requerido para renderizar la tabla, y por default se muestra el botón.
``` javascript
showAddRowButton: {
  type: Boolean,
  required: false,
  default: true
},
```
* **showDeleteRowButton** : Recibe un Boolean indicando si se muestra el botón para eliminar filas. No es requerido para renderizar la tabla, y por default se muestra el botón.
``` javascript
showDeleteRowButton: {
  type: Boolean,
  required: false,
  default: true
},
```
* **iconClassForDeleteButton** : Recibe un String con la clase de icono que se quiera usar como botón para elimnar una fila. No es requerido para renderizar la tabla, y por default usa ```fa fa-trash x2``` de **Font Awesome**.
``` javascript
iconClassForDeleteButton: {
  type: String,
  required: false
},
```
* **iconClassForAddButton** : Recibe un String con la clase de icono que se quiera usar como botón para agregar una fila. No es requerido para renderizar la tabla, y por default usa ```fa fa-plus-square x2``` de **Font Awesome**.
``` javascript
iconClassForAddButton: {
  type: String,
  required: false
},
```
* **data** : Recibe un Array con el mismo formato que **rows** con la data que viene de la Base de Datos.
``` javascript
data: {
  type: Array,
  required: false
}
```
---
## Tipos de columnas

### Selector (dropdown menú)
  * **name**: Un String que es el nombre de la columna.
  * **type**: Para hacer que la columna sea de tipo Selector usar ```'select'```.
  * **placeholder**: Por default es ```'Select an option'```, se puede cambiar por el que uno deseé.
  * **optionsList**: Un Array con las opciones de menú.

### TextInput
  * **name**: Un String que es el nombre de la columna.
  * **type**: Para hacer que la columna sea de tipo TextInput usar  ```'textInput'```.
  * **placeholder**: Por default es ```'Write here...'```, se puede cambiar, se puede cambiar por el que uno deseé.
  * **inputType**: Tipo de input, por default es ```'text'```, se puede cambiar a ```'number'```.
  * **disabled**: Para hacer que input esté deshabilitado, por default esta en ```false```, se puede cambiar a ```true```.

### Checkbox (el desarrollo)  

* **name**: Un String que es el nombre de la columna.
* **type**: Para hacer que la columna sea de tipo Checkbox usar ```'checkbox'```.
* **labelTexts**: Un Array con Strings que van a ser los labels de cada checkbox.
* **checkboxType**: Tipo del checkbox, por default es ```'checkbox'```, se puede cambiar a ```'radio'```.

---
## Eventos  

  ### Selector  
  * **selectedOption**: Devuelve un objeto con la columna y el valor
  ``` javascript
  {column: "select_column", value: 1}
  ```  


  ### TextInput
  * **textInputValue**: Devuelve un objecto con la columna y el valor
  ``` javascript
  {column: "textInput_column", value: "hello"}
  {column: "textInput_number_column", value: "23"}
  ```


  ### Checkbox  
  * **checkboxValue**: Devuelve un objecto con la columna, el index del checkbox y el valor
  ``` javascript
  {column: "checkbox_column", value: true, idxCheck: 0}
  {column: "checkbox_column", value: true, idxCheck: 1}
  {column: "checkbox_column", value: false, idxCheck: 2}
  ```
---
## Ejemplos de usos

* #### Tabla con una columna de tipo selector
  ![tabla de una columna de tipo Selector](./images/table_select_example.png)
  ``` html
  <DynamicTable
    :columns="this.columnsForTableOne()"
    :rows="this.rowsForTableOne"
    :data="this.dataForTableOne"
    v-on:addRow="addRow()"
    v-on:selectedOption="setSelectedOption($event)"
    v-on:deleteRow="deleteRow($event)">
  </DynamicTable>
  ```
  ``` javascript
  data () {
    return {
      rowsForTableOne: [], // Un Array vacío por que no tiene ninguna fila.
      objectDataTableOne: { // Definimos como va a hacer el Objeto que representa a una fila.
        select_column: []
      }
    }
  },
  ```
**Una Columna de tipo Selector se declara como un Objecto con las siguientes propiedades:**  
  * **name**: Es un String con el nombre de la columna. Si el nombre tiene más de una palabra se deben separar con guiones bajos.  
  * **type** : Es un String con el tipo de columna.  
  * **placeholder** : Es un String para definir un placeholder. No es obligatorio definirlo.
  * **optionsList** : Es un Array con las opciones que va a tener el selector.
``` javascript
methods: {
  columnsForTableOne () {
    return [
      {
        name: 'select_column',
        type: 'select',
        placeholder: 'Select an option for this column',
        optionsList: this.optionsListForTable
      }
    ]
  },
}
```  

  **Para agregar una fila agregamos un elemento de fila a rows**  
  ``` javascript
      this.rowsForTableOne.push({
        select_column: null
      })
  ```  
  Al eliminar una fila la tabla ya la elimina automáticamente, si queremos hacer algo más, al momento de eliminarla al escuchar el evento ```deleteRow``` podemos realizar eso que queramos.  
  ``` javascript
  deleteRow (rowIndex) {
    // hacemos lo que queremos. El $event que emite la tabla es el el index de la fila.
  }
  ```  
Para guardar el valor de la opción que se seleccionó escuchamos el evento ```selectedOption```.  
``` javascript
setSelectedOption (option) {
    this.objectDataTableOne[option.column] = option.value
}
```  
* #### Tabla con tres columnas de tipo TextInput
![tabla con tres columnas de tipo TextInput](./images/table_input_example.png)  
``` html
<DynamicTable
    :columns="this.columnsForTableTwo()"
    :rows="this.rowsForTableTwo"
    :data="this.dataForTableTwo"
    v-on:addRow="addRow()"
    v-on:textInputValue="setTextInputValue($event)"
    v-on:deleteRow="deleteRow($event)">
</DynamicTable>
```
``` javascript
data () {
  return {
    rowsForTableTwo: [], // Array de filas
    objectDataTableTwo: { // Objeto que representa una fila
      textInput_column: null,
      textInput_number_column: null,
      textInput_disable_column: null
    }
  }
}
```
**Una Columna de tipo TextInput se declara como un Objecto con las siguientes propiedades:**
