# data-table-vue

This materialize vue data table provides you freedom of customizing anything and everything of your choice.
This data table for vue js is made of plain html5 and plain css without any dependency and gives you flexibility to configure with very minimal yet powerful options


## Install
```
npm i data-table-vue
```

## Attributes and Usage

<table>
<tr>
<th>Attributes</th>
<th>Type</th>
<th>Description</th>
</tr>
<tr>
<td>'fields'</td>
<td>Array of Objects</td>
<td>Each Object must contain 'name' -> To display as header of the Column<br>
Each Object must contain 'key' -> This is use to fetch the value from overall json object of rows
                For example: if you have provide {key:id}, then data-table-vue will loop all the values and try to find the 'id' in each of the object to display under each row.<br>
                Each Object must contain 'sortable' -> Boolean (If true then that column will be allowed as           sortable otherwise not)<br>
                 Optional - 'filterable' -> Boolean (If true then that column will be allowed as           filtering option otherwise not, by default it is true)<br>
                  Optional - 'type' -> String (If 'html' - then that column will render html content, by default it is normal text display)<br>
                Optional -  'sortkey' -> String - This is useful when you are using any inner key value in key. For eg: status.key in this case the actual column value is status_id which is foreign key but you want to display as status.name, wherein at the time of sorting you may need exact column key instead of foreign key, so provide this value as 'status_id'</td>
</tr>
<tr>
<td>'loadEntries'</td>
<td>Object containing three keys</td>
<td>'status' : 200 for success otherwise data-table-vue will consider it as failed.<br>
 'msg'    : Array of Object -> pass list of rows returned by database service.
 <br>'count'  : Numeric -> Total number of overall records present in database.</td>
</tr>
<tr>
<td>'defaultSort'</td>
<td>String</td>
<td>Default Sorted column when data-table-vue loads. Its value should be one of the 'key' passed under 'fields' props</td>
</tr>
<tr>
<td>'defaultSortDir'</td>
<td>'asc' or 'desc'</td>
<td>This is the default sorting direction for default sorted column provided above.</td>
</tr>
<tr>
<td>'defaultSearchColumns'</td>
<td>Array of columns keys</td>
<td>This is the default searching columns on which search has to be performed (List must contain unique keys of the column - same as 'key' property of 'fields' attribute)</td>
</tr>
<tr>
<td>'search'</td>
<td>Boolean</td>
<td>This flag is useful to hide and show the search box. Default: true, if you want to hide the search box then pass false</td>
</tr>
<tr>
<td>'showColumnFilter'</td>
<td>Boolean</td>
<td>This flag is useful to hide and show the selected columns. Default: false, if you want to show the filter option where user can select which columns they want to see, then pass it as true</td>
</tr>
<tr>
<td>'showColumnFilterNotification'</td>
<td>Boolean</td>
<td>This flag is useful to hide and show the number of selected columns as notification. Default: false, if you want to show the notification option, then pass it as true</td>
</tr>
<tr>
<td>'showSearchFilter'</td>
<td>Boolean</td>
<td>This flag is useful to hide and show the searchable columns. Default: false, if you want to show the filter option where user can select which columns they want to search, then pass it as true</td>
</tr>
<tr>
<td>'showSearchFilterNotification'</td>
<td>Boolean</td>
<td>This flag is useful to hide and show the number of searchable columns as notification. Default: false, if you want to show the notification option, then pass it as true</td>
</tr>
<tr>
<td>'searchByFilterName'</td>
<td>String</td>
<td>Name within the search by button</td>
</tr>
<tr>
<td>'columnFilterName'</td>
<td>String</td>
<td>Name within the 'view by' button</td>
</tr>
<tr>
<td>'tableTitle'</td>
<td>String (Optional)</td>
<td>Title of the table</td>
</tr>
<tr>
<td>'actions'</td>
<td>Boolean</td>
<td>If you want action column to be added extra then pass true otherwise false.</td>
</tr>
<tr>
<td>'actionList'</td>
<td>Array of Objects</td>
<td>If you have opted for 'actions' column then you have to pass this field. Each object must contain.<br>
'type' : String -> Currently allowed types are 'link' or 'cb'<br>'refAddress': Function -> recieves particular row data and must return url as String (if type is 'link') or incase of type as 'cb', pass any function which is capable of recieving particular row data and inside your function you can do whatever you want.<br>'icon' : String -> Pass icon name as per materialize icon, for ex: pass 'edit' to show pencil<br>'getIcon' : Function -> Pass icon name as per materialize icon, for ex: pass 'edit' to show pencil. you will recieve particular row as parameter in this function and you can return icon name based on your business logic.<br>
'html' : String -> Currently allowed types are 'true' or 'false', if true, then you have to pass html content in getIcon function</td>
</tr>
<tr>
<td>'perPageOptions'</td>
<td>Array of numbers</td>
<td>pass all possible options for selecting number of rows per page.</td>
</tr>
</table>



## Screenshot

<img src="https://drive.google.com/uc?id=17tPGRpEVncgZycVq09Dwi_Q14sloHE-j" alt="screenshot" />

## include Materialize 

If your application is not using materialize then you have to include materialize in your application.
Add materialize js into your index html like below:

```
<script src="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/js/materialize.min.js"></script>
```

Add materialize css
1. If you want to apply materialize css to specific component then add below line into your component's style

 ```
  <style scoped>
    @import url("https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/css/materialize.min.css");
  </style>
```
2. If you want to apply msterialize css for your entire application then add below line into your index.html

```
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/css/materialize.min.css">

```

     

## How to include data-table-vue in vue file? (Sample Code)
```
<template>
  <div>
    <div id="create" class="col s12">
      <div class="card">
        <div class="card-content">
          <div class="row no-margin">
            <div id="viewAll" class="col s12">
              <div class="row no-margin">
                <div class="col s12">
                  <Table
                    :fields="tableComponentData.fields"
                    :loadEntries="loadEntries"
                    defaultSort="id"
                    defaultSortDir="asc"
                    tableTitle="Demo Table"
                    actions="true"
                    :actionList="actionList"
                    :perPageOptions="tableComponentData.perPageOptions"
                    :defaultSearchColumns="['id']"
                    :showColumnFilter="true"
                    :showColumnFilterNotification="true"
                    :showSearchFilter="true"
                    :showSearchFilterNotification="true"
                  ></Table>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import Table from "data-table-vue";

export default {
  components: { Table },
  data() {
    return {
      tableComponentData: {
        perPageOptions: [15, 20],
        fields: [
          {
            name: "ID",
            key: "id",
            sortable: true
          },
          {
            name: "NAME",
            key: "name",
            sortable: true
          }
        ]
      },
      actionList: [
        {
          type: "link",
          refAddress: data => `edit/${data.id}`,
          icon: "edit"
        }
      ]
    };
  },
  mixins: [],
  props: {
    props: Object
  },
  methods: {
    loadEntries(
      start,
      recordsPerPage,
      currentSort = "id",
      currentSortDir = "asc",
      searchText,
      defaultSearchColumns,
      hideLoading,
      cb
    ) {
      let data = {
        status: 200,
        msg: [{ id: 1, name: "name 1" }, { id: 2, name: "name 2" }],
        count: 2
      };
      cb(data);
    }
  }
};
</script>

<style scoped>
@import url("https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/css/materialize.min.css");
</style>

```

