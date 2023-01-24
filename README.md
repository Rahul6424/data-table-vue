# data-table-vue

> - This materialize vue data table provides you freedom of customizing anything and everything of your choice.
> - This data table for vue js is made of plain html5 and plain css without any dependency and gives you flexibility to configure with very minimal yet powerful options

---

## Features

- ✔️ Table works on both **Offline** mode & **Online** mode.
- ✔️ Global **Search** feature.
- ✔️ Individual column based **Filter** feature.
- ✔️ **Sort** mechanism with default sort column on initial load.
- ✔️ Customizable sort **Direction**.
- ✔️ **Show/Hide** columns on the fly.
- ✔️ **Export as CSV** with two options - Filtered data / Unfiltered data (raw data).
- ✔️ Facility to create **Custom buttons**.
- ✔️ **Drag & Drop** feature for columns ordering on the fly.
- ✔️ **Pin/Unpin** feature for columns to make position fixed/scrollable.
- ✔️ **Auto Save** customized table options and it gets applied on next reload as default.
- ✔️ Render table **with/without pagination**
- ️✔️ Pass any number of columns with various customization.
- ✔️ Customizable **"Items / page"** count.
- ✔️ Customizable **"Table Title"**.
- ✔️ Customizable **"Actions"** column.
- ✔️ Customizable **"Actions"** column position (First / Last).

---

# Table of Contents

1. [Quick Start](#quick_start)
2. [How to include data-table-vue](#how_to)
   1. [Basic Table](#basic_table)
   2. [How to add table's title](#table_title)
   3. [How to add Action/Edit column](#action_section)
   4. [Move Action/Edit column towards left](#action_move_left)
   5. [Activate Pagination](#activate_pagination)
   6. [Global Search Box](#global_search)
   7. [Global Search Box on user selected columns](#global_search_custom)
   8. [Show/Hide Columns](#show_hide)
   9. [Export as CSV](#export)
   10. [Rearrange Columns by drag & drop](#rearrange)
   11. [Filter option for individual column](#filter_single)
   12. [Fixed/Pin Columns on left (non-scrollable)](#pinned)
   13. [Memorize locally](#memorize)
   14. [Sortable option on columns](#sortable_all)
3. [Table Props](#table_props)
3. [Custom Buttons](#custom_buttons)

# **<h1 id="quick_start">Quick Start </h1>**

#### **Install**

> - To install the data-table-vue and saving it to package.json dependency
> - Open your favorite Terminal and run below command.

```
npm i data-table-vue --save
```

<br>

#### **Include Materialize CDN**

> - If your application is `not already using` materialize then you have to include materialize in your application.
> - Add materialize js into your **index html** like below:

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/js/materialize.min.js"></script>
```

<br>

#### **Include JQuery CDN**

> - If your application is `not already using` jquery then you have to include jquery in your application.
> - Add JQuery CDN into your **index html** like below:

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.3/jquery.min.js" integrity="sha512-STof4xm1wgkfm7heWqFJVn58Hm3EtS31XFaagaa8VMReCXAkQnJZ+jEy8PCC/iT18dFy95WcExNHFTqLyp72eQ==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
```

<br>

#### **Add materialize css**

> If you want to apply materialize css `to specific component` then add below line into your component's style

```html
 <style scoped>
   @import url("https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/css/materialize.min.css");
 </style>
```

> If you want to apply materialize css for your `entire application` then add below line into your **index.html**

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/css/materialize.min.css">
```

# **<h1 id="how_to">How to include data-table-vue</h1>**

> - Let's imagine you have `App.vue` file where you want to include data-table-vue
> - We will start with `basic setup` and slowly we will cover all the features one by one

#### **<h4 id="basic_table">Script Section </h4>**

> - Let's create basic table with 6 fields.
> - `ID` | `NAME` | `ADDRESS 1` | `ADDRESS 2` | `Mobile No` | `Landline`
> - Here is the **attributes/properties** required to configure basic table

| Attributes         | Data Type        | Mandatory | Purpose                                                                                                                                                                                       |
| ------------------ | ---------------- | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| perPageOptions     | Array            | Yes       | This will generate a dropdown for selecting items per page at the bottom right of the table for pagination and first element will be selected `default` [more...](#per_page_options_attributes) |
| fields             | Array Of Objects | Yes       | This will generate table header. [Click here](#fields_attributes) to know all possible properties                                                                                             |
| loadOfflineEntries | Function         | Yes       | This function must call `callback` argument with the Array of Objects of items as first argument. [Click here](#load_offline_entries_attributes) to know about json structure                   |
| hideSearchBox      | Boolean          | No        | By default the global search box will be visible but if you want to hide the global search box then pass value as `true` [more...](#hide_search_box_attributes)                                 |
| noPagination       | Boolean          | No        | By default the pagination will be visible but if you want to hide the pagination functionality then pass value as `true` [more...](#no_pagination_attributes)                                  |

<br>

```html
<script>
import Table from "data-table-vue"; // import data-table-vue
export default {
 components: { Table }, // declare it as component
 data() {
   return {
     tableComponentData: {
       perPageOptions: [70],
       fields: [
         {
           name: "ID",
           key: "id"
         },
         {
           name: "NAME",
           key: "name"
         },
         {
           name: "ADDRESS 1",
           key: "address"
         },
         {
           name: "ADDRESS 2",
           key: "address1"
         },
         {
           name: "Mobile No",
           key: "mob"
         },
         {
           name: "Landline",
           key: "landline"
         },
       ]
     }
   };
 },
 methods: {
   getData() {
     let randomData = []
     for (let i = 0; i < 10; i++) {
       randomData.push(
           {
               id: i + 1,
               name: `name ${i + 1}`,
               address: `Lorem Ipsum Dolor Sit Amet  ${i + 1}`,
               address1: `address 2 ${i + 1}`,
               mob: `mob_num_dummy_${i + 1}`,
               landline: `landline_dummy_${i + 1}`
           });
     }
     return randomData;
   },
   loadOfflineEntries(
     cb
   ) {
     let data = {
       status: 200,
       msg: this.getData()
     };
     cb(data);
   }
 }
};
</script>
```

#### **Template Section**

```html
<template>
 <div>
   <div class="col s12">
     <div class="card">
       <div class="card-content">
         <div class="row no-margin">
           <div id="viewAll" class="col s12">
             <div class="row no-margin">
               <div class="col s12">
                 <Table
                   :offLineMode="true"
                   :fields="tableComponentData.fields"
                   :loadOfflineEntries="loadOfflineEntries"
                    defaultSort="id"
                    defaultSortDir="asc"
                    tableUniqueId="test_table"
                   :perPageOptions="tableComponentData.perPageOptions"
                   :hideSearchBox="true"
                   :noPagination="true">
                 </Table>
               </div>
             </div>
           </div>
         </div>
       </div>
     </div>
   </div>
 </div>
</template>
```

## Screenshot - Basic Table

![Basic Table](https://github.com/Rahul6424/data-table-vue/blob/master/public/Step-1.png?raw=true "Basic Table")

<br>

#### **<h4 id="table_title">How to add table's title</h4>**

> - Just add [tableTitle](#table_title_attributes) props
> - `Sample code` is shown below

```html
<template>
 <div>
   <div class="col s12">
     <div class="card">
       <div class="card-content">
         <div class="row no-margin">
           <div id="viewAll" class="col s12">
             <div class="row no-margin">
               <div class="col s12">
                 <Table
                   :offLineMode="true"
                   :fields="tableComponentData.fields"
                   :loadOfflineEntries="loadOfflineEntries"
                    defaultSort="id"
                    defaultSortDir="asc"
                    tableUniqueId="test_table"
                   :perPageOptions="tableComponentData.perPageOptions"
                   :hideSearchBox="true"
                   :noPagination="true"
                   tableTitle="Demo Table"
                   >
                 </Table>
               </div>
             </div>
           </div>
         </div>
       </div>
     </div>
   </div>
 </div>
</template>
```

## Screenshot - With Table Title

![Table Title](https://github.com/Rahul6424/data-table-vue/blob/master/public/Step-2.png?raw=true "Table Title")

<br>

#### **<h4 id="action_section">How to add Action/Edit column</h4>**

> 1. Add [actions](#actions_attributes) property in order to show the **Action** column.
> 2. Add [actionList](#action_list_attributes) property.
> 3. `Sample Code` is shown below.

```html
<template>
 <div>
   <div class="col s12">
     <div class="card">
       <div class="card-content">
         <div class="row no-margin">
           <div id="viewAll" class="col s12">
             <div class="row no-margin">
               <div class="col s12">
                 <Table
                   :offLineMode="true"
                   :fields="tableComponentData.fields"
                   :loadOfflineEntries="loadOfflineEntries"
                    defaultSort="id"
                    defaultSortDir="asc"
                    tableUniqueId="test_table"
                   :perPageOptions="tableComponentData.perPageOptions"
                   :hideSearchBox="true"
                   :noPagination="true"
                   tableTitle="Demo Table"
                   actions="true"
                   :actionList="actionList"
                   >
                 </Table>
               </div>
             </div>
           </div>
         </div>
       </div>
     </div>
   </div>
 </div>
</template>
```

#### **<h4>Script Section </h4>**

```html
<script>
import Table from "data-table-vue"; // import data-table-vue
export default {
 components: { Table }, // declare it as component
 data() {
   return {
     tableComponentData: {
       perPageOptions: [70],
       fields: [
         {
           name: "ID",
           key: "id"
         },
         {
           name: "NAME",
           key: "name"
         },
         {
           name: "ADDRESS 1",
           key: "address"
         },
         {
           name: "ADDRESS 2",
           key: "address1"
         },
         {
           name: "Mobile No",
           key: "mob"
         },
         {
           name: "Landline",
           key: "landline"
         },
       ],
        actionList: [
         {
           type: "link",
           refAddress: data => `edit/${data.id}`,
           getIcon: data => 'edit',
           hoverTitle: "Edit Item"
         },
         {
           type: "cb",
           refAddress: data => {
             alert(`Click on row with ID = `, data.id);
           },
           getIcon: data => '<i class="material-icons">add</i>',
           html: "true",
         }
       ]
     }
   };
 },
 methods: {
   getData() {
     let randomData = []
     for (let i = 0; i < 10; i++) {
       randomData.push(
           {
               id: i + 1,
               name: `name ${i + 1}`,
               address: `Lorem Ipsum Dolor Sit Amet  ${i + 1}`,
               address1: `address 2 ${i + 1}`,
               mob: `mob_num_dummy_${i + 1}`,
               landline: `landline_dummy_${i + 1}`
           });
     }
     return randomData;
   },
   loadOfflineEntries(
     cb
   ) {
     let data = {
       status: 200,
       msg: this.getData()
     };
     cb(data);
   }
 }
};
</script>
```

## Screenshot - With Action Column

![Action Column](https://github.com/Rahul6424/data-table-vue/blob/master/public/Step-3.png?raw=true "Action Column")

<br>

#### **<h4 id="action_move_left">Move Action/Edit column towards left</h4>**

> - Just add [fixedActionColumnOnLeft](#fixed_action_column_on_left_attributes) props
> - `Sample code` is shown below

```html
<template>
 <div>
   <div class="col s12">
     <div class="card">
       <div class="card-content">
         <div class="row no-margin">
           <div id="viewAll" class="col s12">
             <div class="row no-margin">
               <div class="col s12">
                 <Table
                   :offLineMode="true"
                   :fields="tableComponentData.fields"
                   :loadOfflineEntries="loadOfflineEntries"
                    defaultSort="id"
                    defaultSortDir="asc"
                    tableUniqueId="test_table"
                   :perPageOptions="tableComponentData.perPageOptions"
                   :hideSearchBox="true"
                   :noPagination="true"
                   tableTitle="Demo Table"
                   actions="true"
                   :actionList="actionList"
                   :fixedActionColumnOnLeft="true"
                   >
                 </Table>
               </div>
             </div>
           </div>
         </div>
       </div>
     </div>
   </div>
 </div>
</template>
```

## Screenshot - With Action column towards left

![Action column towards left](https://github.com/Rahul6424/data-table-vue/blob/master/public/Step-4.png?raw=true "Action column towards left")

<br>

#### **<h4 id="activate_pagination">Activate Pagination</h4>**

> Just remove [noPagination](#no_pagination_attributes) props or simply make its value to `false` > `Sample code` is shown below

```html
<template>
 <div>
   <div class="col s12">
     <div class="card">
       <div class="card-content">
         <div class="row no-margin">
           <div id="viewAll" class="col s12">
             <div class="row no-margin">
               <div class="col s12">
                 <Table
                   :offLineMode="true"
                   :fields="tableComponentData.fields"
                   :loadOfflineEntries="loadOfflineEntries"
                    defaultSort="id"
                    defaultSortDir="asc"
                    tableUniqueId="test_table"
                   :perPageOptions="tableComponentData.perPageOptions"
                   :hideSearchBox="true"
                   tableTitle="Demo Table"
                   actions="true"
                   :actionList="actionList"
                   :fixedActionColumnOnLeft="true"
                   >
                 </Table>
               </div>
             </div>
           </div>
         </div>
       </div>
     </div>
   </div>
 </div>
</template>
```

## Screenshot - With Pagination on bottom right

![Pagination on bottom right](https://github.com/Rahul6424/data-table-vue/blob/master/public/Step-5.png?raw=true "Pagination on bottom right")

<br>

#### **<h4 id="global_search">Global Search Box</h4>**

> - Just remove [hideSearchBox](#hide_search_box_attributes) props or simply make its value to `false`
> - Also add [defaultSearchColumns](#default_search_columns_attributes) props.
> - `Sample code` is shown below where we are making `Global Search` upon two columns i.e. `id` & `name`

```html
<template>
 <div>
   <div class="col s12">
     <div class="card">
       <div class="card-content">
         <div class="row no-margin">
           <div id="viewAll" class="col s12">
             <div class="row no-margin">
               <div class="col s12">
                 <Table
                   :offLineMode="true"
                   :fields="tableComponentData.fields"
                   :loadOfflineEntries="loadOfflineEntries"
                    defaultSort="id"
                    defaultSortDir="asc"
                    tableUniqueId="test_table"
                   :perPageOptions="tableComponentData.perPageOptions"
                   :hideSearchBox="false"
                   tableTitle="Demo Table"
                   actions="true"
                   :actionList="actionList"
                   :defaultSearchColumns="['id', 'name']"
                   >
                 </Table>
               </div>
             </div>
           </div>
         </div>
       </div>
     </div>
   </div>
 </div>
</template>
```

## Screenshot - With Global Search Box

![Pagination on bottom right](https://github.com/Rahul6424/data-table-vue/blob/master/public/Step-6.png?raw=true "Pagination on bottom right")

<br>

#### **<h4 id="global_search_custom">Global Search Box on user selected columns</h4>**

> - Add [showSearchFilter](#show_search_filter_attributes) props.
> - (Optional) You can also choose the `Title` of [searchByFilterName](#search_by_filter_name_attributes) popup.
> - (Optional) You can also choose the `Notification Count` of [showSearchFilterNotification](#show_search_filter_notification_attributes).
> - `Sample code` is shown below where `Global Search` will be activated on default columns i.e. `id` & `name` but there will be an extra option provided where user can select on which all columns `Global Search` should work from UI.

```html
<template>
 <div>
   <div class="col s12">
     <div class="card">
       <div class="card-content">
         <div class="row no-margin">
           <div id="viewAll" class="col s12">
             <div class="row no-margin">
               <div class="col s12">
                 <Table
                   :offLineMode="true"
                   :fields="tableComponentData.fields"
                   :loadOfflineEntries="loadOfflineEntries"
                    defaultSort="id"
                    defaultSortDir="asc"
                    tableUniqueId="test_table"
                   :perPageOptions="tableComponentData.perPageOptions"
                   :hideSearchBox="false"
                   tableTitle="Demo Table"
                   actions="true"
                   :actionList="actionList"
                   :defaultSearchColumns="['id', 'name']"
                   :showSearchFilter="true"
                   searchByFilterName="This is Filter Title"
                   :showSearchFilterNotification="true"
                   >
                 </Table>
               </div>
             </div>
           </div>
         </div>
       </div>
     </div>
   </div>
 </div>
</template>
```

## Screenshot - With Global Search Box on user selected columns

![Global Search Box on user selected columns](https://github.com/Rahul6424/data-table-vue/blob/master/public/Step-7.png?raw=true "Global Search Box on user selected columns")

<br>

#### **<h4 id="show_hide">Show/Hide Columns</h4>**

> - Add [showColumnFilter](#show_column_filter_attributes) props.
> - (Optional) You can also choose the `Title` of [columnFilterName](#column_filter_name_attributes) popup.
> - (Optional) You can also choose the `Notification Count` of [showColumnFilterNotification](#show_column_filter_notification_attributes).
> - `Sample code` is shown below.

```html
<template>
 <div>
   <div class="col s12">
     <div class="card">
       <div class="card-content">
         <div class="row no-margin">
           <div id="viewAll" class="col s12">
             <div class="row no-margin">
               <div class="col s12">
                 <Table
                   :offLineMode="true"
                   :fields="tableComponentData.fields"
                   :loadOfflineEntries="loadOfflineEntries"
                    defaultSort="id"
                    defaultSortDir="asc"
                    tableUniqueId="test_table"
                   :perPageOptions="tableComponentData.perPageOptions"
                   :hideSearchBox="false"
                   tableTitle="Demo Table"
                   actions="true"
                   :actionList="actionList"
                   :defaultSearchColumns="['id', 'name']"
                   :showSearchFilter="true"
                   searchByFilterName="This is Filter Title"
                   :showSearchFilterNotification="true"
                   :showColumnFilter="true"
                   columnFilterName="This is column show/hide options"
                   :showColumnFilterNotification="true"
                   >
                 </Table>
               </div>
             </div>
           </div>
         </div>
       </div>
     </div>
   </div>
 </div>
</template>
```

## Screenshot - With Show/Hide Columns filter

![Show/Hide Columns filter](https://github.com/Rahul6424/data-table-vue/blob/master/public/Step-8.png?raw=true "Show/Hide Columns filter")

<br>

#### **<h4 id="export">Export as CSV</h4>**

> - Add [exportExcel](#export_excel_attributes) props.
> - `Sample code` is shown below.

```html
<template>
 <div>
   <div class="col s12">
     <div class="card">
       <div class="card-content">
         <div class="row no-margin">
           <div id="viewAll" class="col s12">
             <div class="row no-margin">
               <div class="col s12">
                 <Table
                   :offLineMode="true"
                   :fields="tableComponentData.fields"
                   :loadOfflineEntries="loadOfflineEntries"
                    defaultSort="id"
                    defaultSortDir="asc"
                    tableUniqueId="test_table"
                   :perPageOptions="tableComponentData.perPageOptions"
                   :hideSearchBox="false"
                   tableTitle="Demo Table"
                   actions="true"
                   :actionList="actionList"
                   :defaultSearchColumns="['id', 'name']"
                   :showSearchFilter="true"
                   searchByFilterName="This is Filter Title"
                   :showSearchFilterNotification="true"
                   :showColumnFilter="true"
                   columnFilterName="This is column show/hide options"
                   :showColumnFilterNotification="true"
                   :exportExcel="true"
                   >
                 </Table>
               </div>
             </div>
           </div>
         </div>
       </div>
     </div>
   </div>
 </div>
</template>
```

## Screenshot - With Export as CSV option

![Export as CSV option](https://github.com/Rahul6424/data-table-vue/blob/master/public/Step-9.png?raw=true "Export as CSV option")

<br>

#### **<h4 id="rearrange">Rearrange Columns by drag & drop</h4>**

> - Add [moveableColumn](#moveable_column_attributes) props.
> - `Sample code` is shown below.

```html
<template>
 <div>
   <div class="col s12">
     <div class="card">
       <div class="card-content">
         <div class="row no-margin">
           <div id="viewAll" class="col s12">
             <div class="row no-margin">
               <div class="col s12">
                 <Table
                   :offLineMode="true"
                   :fields="tableComponentData.fields"
                   :loadOfflineEntries="loadOfflineEntries"
                    defaultSort="id"
                    defaultSortDir="asc"
                    tableUniqueId="test_table"
                   :perPageOptions="tableComponentData.perPageOptions"
                   :hideSearchBox="false"
                   tableTitle="Demo Table"
                   actions="true"
                   :actionList="actionList"
                   :defaultSearchColumns="['id', 'name']"
                   :showSearchFilter="true"
                   searchByFilterName="This is Filter Title"
                   :showSearchFilterNotification="true"
                   :showColumnFilter="true"
                   columnFilterName="This is column show/hide options"
                   :showColumnFilterNotification="true"
                   :exportExcel="true"
                   :moveableColumn="true"
                   >
                 </Table>
               </div>
             </div>
           </div>
         </div>
       </div>
     </div>
   </div>
 </div>
</template>
```

## Screenshot - With Rearrange Columns

![Rearrange Columns](https://github.com/Rahul6424/data-table-vue/blob/master/public/Step-10.png?raw=true "Rearrange Columns")

<br>

#### **<h4 id="filter_single">Filter option for individual column</h4>**

> - Add [showColumnFilterButton](#show_column_filter_button_attributes) props.
> - Add `multiFilterOption` property on [fields](#fields_attributes) on those columns where you want to filter.
> - `Sample code` is shown below, where we are making filterable columns as `ADDRESS 1` & `ADDRESS 2`.

```html
<template>
 <div>
   <div class="col s12">
     <div class="card">
       <div class="card-content">
         <div class="row no-margin">
           <div id="viewAll" class="col s12">
             <div class="row no-margin">
               <div class="col s12">
                 <Table
                   :offLineMode="true"
                   :fields="tableComponentData.fields"
                   :loadOfflineEntries="loadOfflineEntries"
                    defaultSort="id"
                    defaultSortDir="asc"
                    tableUniqueId="test_table"
                   :perPageOptions="tableComponentData.perPageOptions"
                   :hideSearchBox="false"
                   tableTitle="Demo Table"
                   actions="true"
                   :actionList="actionList"
                   :defaultSearchColumns="['id', 'name']"
                   :showSearchFilter="true"
                   searchByFilterName="This is Filter Title"
                   :showSearchFilterNotification="true"
                   :showColumnFilter="true"
                   columnFilterName="This is column show/hide options"
                   :showColumnFilterNotification="true"
                   :exportExcel="true"
                   :moveableColumn="true"
                   :showColumnFilterButton="true"
                   >
                 </Table>
               </div>
             </div>
           </div>
         </div>
       </div>
     </div>
   </div>
 </div>
</template>
```

#### **<h4>Script Section </h4>**

```html
<script>
import Table from "data-table-vue"; // import data-table-vue
export default {
 components: { Table }, // declare it as component
 data() {
   return {
     tableComponentData: {
       perPageOptions: [70],
       fields: [
         {
           name: "ID",
           key: "id"
         },
         {
           name: "NAME",
           key: "name"
         },
         {
           name: "ADDRESS 1",
           key: "address",
           multiFilterOption: true
         },
         {
           name: "ADDRESS 2",
           key: "address1",
           multiFilterOption: true
         },
         {
           name: "Mobile No",
           key: "mob"
         },
         {
           name: "Landline",
           key: "landline"
         },
       ],
        actionList: [
         {
           type: "link",
           refAddress: data => `edit/${data.id}`,
           getIcon: data => 'edit',
           hoverTitle: "Edit Item"
         },
         {
           type: "cb",
           refAddress: data => {
             alert(`Click on row with ID = `, data.id);
           },
           getIcon: data => '<i class="material-icons">add</i>',
           html: "true",
         }
       ]
     }
   };
 },
 methods: {
   getData() {
     let randomData = []
     for (let i = 0; i < 10; i++) {
       randomData.push(
           {
               id: i + 1,
               name: `name ${i + 1}`,
               address: `Lorem Ipsum Dolor Sit Amet  ${i + 1}`,
               address1: `address 2 ${i + 1}`,
               mob: `mob_num_dummy_${i + 1}`,
               landline: `landline_dummy_${i + 1}`
           });
     }
     return randomData;
   },
   loadOfflineEntries(
     cb
   ) {
     let data = {
       status: 200,
       msg: this.getData()
     };
     cb(data);
   }
 }
};
</script>
```

## Screenshot - With Filter option for individual column

![Filter option for individual column](https://github.com/Rahul6424/data-table-vue/blob/master/public/Step-11.png?raw=true "Filter option for individual column")

<br>

#### **<h4 id="pinned">Fixed/Pin Columns on left (non-scrollable)</h4>**

> - Add [showLockColumnsButton](#show_lock_columns_button_attributes) props.
> - Add `lockable` property in [fields](#fields_attributes) on those columns where you want to lock.
> - Add `lock` property in [fields](#fields_attributes) on those columns where `lockable` is true. This is mandatory when `lockable` is true.
> - `Sample code` is shown below, where we are making lockable columns as `id` & `name`, in which `id` column is `locked` by default whereas `name` column doesn't.

```html
<template>
 <div>
   <div class="col s12">
     <div class="card">
       <div class="card-content">
         <div class="row no-margin">
           <div id="viewAll" class="col s12">
             <div class="row no-margin">
               <div class="col s12">
                 <Table
                   :offLineMode="true"
                   :fields="tableComponentData.fields"
                   :loadOfflineEntries="loadOfflineEntries"
                    defaultSort="id"
                    defaultSortDir="asc"
                    tableUniqueId="test_table"
                   :perPageOptions="tableComponentData.perPageOptions"
                   :hideSearchBox="false"
                   tableTitle="Demo Table"
                   actions="true"
                   :actionList="actionList"
                   :defaultSearchColumns="['id', 'name']"
                   :showSearchFilter="true"
                   searchByFilterName="This is Filter Title"
                   :showSearchFilterNotification="true"
                   :showColumnFilter="true"
                   columnFilterName="This is column show/hide options"
                   :showColumnFilterNotification="true"
                   :exportExcel="true"
                   :moveableColumn="true"
                   :showColumnFilterButton="true"
                   :showLockColumnsButton="true"
                   >
                 </Table>
               </div>
             </div>
           </div>
         </div>
       </div>
     </div>
   </div>
 </div>
</template>
```

#### **<h4>Script Section </h4>**

```html
<script>
import Table from "data-table-vue"; // import data-table-vue
export default {
 components: { Table }, // declare it as component
 data() {
   return {
     tableComponentData: {
       perPageOptions: [70],
       fields: [
         {
           name: "ID",
           key: "id",
           lockable:true,
           lock:true // this is mandatory if lockable is true and lock:true means this column will be locked by default
         },
         {
           name: "NAME",
           key: "name",
           lockable:true,
           lock:false // this is mandatory if lockable is true and lock:false means this column will be not be locked by default
         },
         {
           name: "ADDRESS 1",
           key: "address",
           multiFilterOption: true
         },
         {
           name: "ADDRESS 2",
           key: "address1",
           multiFilterOption: true
         },
         {
           name: "Mobile No",
           key: "mob"
         },
         {
           name: "Landline",
           key: "landline"
         },
       ],
        actionList: [
         {
           type: "link",
           refAddress: data => `edit/${data.id}`,
           getIcon: data => 'edit',
           hoverTitle: "Edit Item"
         },
         {
           type: "cb",
           refAddress: data => {
             alert(`Click on row with ID = `, data.id);
           },
           getIcon: data => '<i class="material-icons">add</i>',
           html: "true",
         }
       ]
     }
   };
 },
 methods: {
   getData() {
     let randomData = []
     for (let i = 0; i < 10; i++) {
       randomData.push(
           {
               id: i + 1,
               name: `name ${i + 1}`,
               address: `Lorem Ipsum Dolor Sit Amet  ${i + 1}`,
               address1: `address 2 ${i + 1}`,
               mob: `mob_num_dummy_${i + 1}`,
               landline: `landline_dummy_${i + 1}`
           });
     }
     return randomData;
   },
   loadOfflineEntries(
     cb
   ) {
     let data = {
       status: 200,
       msg: this.getData()
     };
     cb(data);
   }
 }
};
</script>
```

## Screenshot - With Fixed/Pin Columns on left (non-scrollable)

![Fixed/Pin Columns on left (non-scrollable)](https://github.com/Rahul6424/data-table-vue/blob/master/public/Step-12.png?raw=true "Fixed/Pin Columns on left (non-scrollable)")

<br>

#### **<h4 id="memorize">Memorize locally - all changes Ex: Filtered, Rearraged columns, default number of items / page etc.</h4>**

> - Add [memorizeSettingsLocally](#memorize_settings_locally_attributes) props.
> - `Sample code` is shown below.

```html
<template>
 <div>
   <div class="col s12">
     <div class="card">
       <div class="card-content">
         <div class="row no-margin">
           <div id="viewAll" class="col s12">
             <div class="row no-margin">
               <div class="col s12">
                 <Table
                   :offLineMode="true"
                   :fields="tableComponentData.fields"
                   :loadOfflineEntries="loadOfflineEntries"
                    defaultSort="id"
                    defaultSortDir="asc"
                    tableUniqueId="test_table"
                   :perPageOptions="tableComponentData.perPageOptions"
                   :hideSearchBox="false"
                   tableTitle="Demo Table"
                   actions="true"
                   :actionList="actionList"
                   :defaultSearchColumns="['id', 'name']"
                   :showSearchFilter="true"
                   searchByFilterName="This is Filter Title"
                   :showSearchFilterNotification="true"
                   :showColumnFilter="true"
                   columnFilterName="This is column show/hide options"
                   :showColumnFilterNotification="true"
                   :exportExcel="true"
                   :moveableColumn="true"
                   :showColumnFilterButton="true"
                   :showLockColumnsButton="true"
                   :memorizeSettingsLocally="true"
                   >
                 </Table>
               </div>
             </div>
           </div>
         </div>
       </div>
     </div>
   </div>
 </div>
</template>
```

## Screenshot - With Memorize locally

![Memorize](https://github.com/Rahul6424/data-table-vue/blob/master/public/Step-13.png?raw=true "Memorize")

<br>

#### **<h4 id="sortable_all">Sortable option on columns</h4>**

> - Add `sortable` property in [fields](#fields_attributes) on those columns which you want it to be sortable.
> - `Sample code` is shown below, where we are making sortable columns as `ID`, `NAME`, `ADDRESS 1` & `ADDRESS 2`.

```html
<template>
 <div>
   <div class="col s12">
     <div class="card">
       <div class="card-content">
         <div class="row no-margin">
           <div id="viewAll" class="col s12">
             <div class="row no-margin">
               <div class="col s12">
                 <Table
                   :offLineMode="true"
                   :fields="tableComponentData.fields"
                   :loadOfflineEntries="loadOfflineEntries"
                    defaultSort="id"
                    defaultSortDir="asc"
                    tableUniqueId="test_table"
                   :perPageOptions="tableComponentData.perPageOptions"
                   :hideSearchBox="false"
                   tableTitle="Demo Table"
                   actions="true"
                   :actionList="actionList"
                   :defaultSearchColumns="['id', 'name']"
                   :showSearchFilter="true"
                   searchByFilterName="This is Filter Title"
                   :showSearchFilterNotification="true"
                   :showColumnFilter="true"
                   columnFilterName="This is column show/hide options"
                   :showColumnFilterNotification="true"
                   :exportExcel="true"
                   :moveableColumn="true"
                   :showColumnFilterButton="true"
                   :showLockColumnsButton="true"
                   >
                 </Table>
               </div>
             </div>
           </div>
         </div>
       </div>
     </div>
   </div>
 </div>
</template>
```

#### **<h4>Script Section </h4>**

```html
<script>
import Table from "data-table-vue"; // import data-table-vue
export default {
 components: { Table }, // declare it as component
 data() {
   return {
     tableComponentData: {
       perPageOptions: [5, 10, 15],
       fields: [
         {
           name: "ID",
           key: "id",
           lockable: true,
           lock: true,
           sortable: true
         },
         {
           name: "NAME",
           key: "name",
           lockable: true,
           lock: false,
           sortable: true
         },
         {
           name: "ADDRESS 1",
           key: "address",
           multiFilterOption: true,
           sortable: true
         },
         {
           name: "ADDRESS 2",
           key: "address1",
           multiFilterOption: true,
           sortable: true
         },
         {
           name: "Mobile No",
           key: "mob"
         },
         {
           name: "Landline",
           key: "landline"
         },
       ],
        actionList: [
         {
           type: "link",
           refAddress: data => `edit/${data.id}`,
           getIcon: data => 'edit',
           hoverTitle: "Edit Item"
         },
         {
           type: "cb",
           refAddress: data => {
             alert(`Click on row with ID = `, data.id);
           },
           getIcon: data => '<i class="material-icons">add</i>',
           html: "true",
         }
       ]
     }
   };
 },
 methods: {
   getData() {
     let randomData = []
     for (let i = 0; i < 10; i++) {
       randomData.push(
           {
               id: i + 1,
               name: `name ${i + 1}`,
               address: `Lorem Ipsum Dolor Sit Amet  ${i + 1}`,
               address1: `address 2 ${i + 1}`,
               mob: `mob_num_dummy_${i + 1}`,
               landline: `landline_dummy_${i + 1}`
           });
     }
     return randomData;
   },
   loadOfflineEntries(
     cb
   ) {
     let data = {
       status: 200,
       msg: this.getData()
     };
     cb(data);
   }
 }
};
</script>
```

## Screenshot - With Sortable option on columns

![Sortable option on columns](https://github.com/Rahul6424/data-table-vue/blob/master/public/Step-14.png?raw=true "Sortable option on columns")

# **<h1 id="table_props">Table Props</h1>**

> Below are the list of all possible attributes of data-table-vue

**<h2 id="table_unique_id_attributes">tableUniqueId: String</h2>**

> - Must be passed as props
> - Value should be unique identifier between multiple `data-table-vue` and must not contain any `space` or `hyphen(-)`

<br>

**<h2 id="table_title_attributes">tableTitle: String</h2>**

> - This property will start displaying the `Table Title` on top left corner.
> - `Don't` pass this property if you don't need table title.

<br>

**<h2 id="offline_mode_attributes">offLineMode : Boolean</h2>**

> Must be passed as props
>
> 1. If value is`true` then the table will work in offline mode i.e. pagination, filter, search etc. will be calculated on browser side and no APIs will be called.
> 2. If value is `false` then the table will work as live mode i.e. pagination, filter, search etc. will not be calculated on browser, rather respective APIs will be called to get information.

<br>

**<h2 id="per_page_options_attributes">perPageOptions: Array of Number(s)</h2>**

> - Must be passed as props
> - This will generate a dropdown for selecting items per page at the bottom right of the table for pagination
> - First element will be selected as `default`

<br>

**<h2 id="hide_search_box_attributes">hideSearchBox: Boolean</h2>**

> By default the global search box will be visible but if you want to hide the global search box then pass value as `true`

<br>

**<h2 id="no_pagination_attributes">noPagination: Boolean</h2>**

> By default the pagination will be visible but if you want to hide the pagination functionality then pass value as `true`

<br>

**<h2 id="fields_attributes">fields : Array of Objects</h2>**

> - This will generate the `Table Header`
> - Each object should contain appropriate keys mentioned below

| Properties        | Data Type | Mandatory | Purpose                                                                                                                                                                                                                                  |
| ----------------- | --------- | --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| name              | String    | Yes       | This property will be used as display text in header                                                                                                                                                                                     |
| key               | String    | Yes       | unique identifier of the property and `it should not contain any spaces or hyphens`                                                                                                                                                      |
| multiFilterOption | Boolean   | No        | This property will provide an option to perform `column based filter` at column header.                                                                                                                                                  |
| lockable          | Boolean   | No        | This property will provide an option to perform `column based lock/pin` at column header.                                                                                                                                                |
| lock              | Boolean   | No        | This property will make respective column `Locked/Pinned` by default.<br>This property is mandatory when `lockable` is true.<br>If you want to make column as `Locked/Pinned` by default then provide value as `true` otherwise `false`. |
| defaultValue      | String    | No        | Incase if value is not available in the entries then this value will be used to display the content for specific column and row.                                                                                                         |
| sortable          | Boolean   | No        | If true then respective column will be allowed as sortable otherwise not.                                                                                                                                                                |
| sortkey           | String    | No        | If true then respective column will be allowed as sortable otherwise not.                                                                                                                                                                |
| filterable        | Boolean   | No        | If true then respective column will be allowed as filterable otherwise not, by default it is true.                                                                                                                                       |
| type              | String    | No        | If `'html'` - then respective column's data will be considered as `html content` and it will be rendered as html, `by default` it is `normal text` display.                                                                              |
| sortkey           | String    | No        | This will be helpful when you want to display the content with other key whereas while `sorting` you want to sort `with different key`, then provide sorting key as value.                                                               |
| filterkey         | String    | No        | This will be helpful when you want to display the content with other key whereas while `searching` you want to sort `with different key`, then provide searching key as value.                                                           |

<br>

**<h2 id="load_offline_entries_attributes">loadOfflineEntries : Function</h2>**

> - This is the first function which will be called when data-vue-table loads.
> - In this function you can call your API to get the table data.
> - This function will be called if [offLineMode](#offline_mode_attributes) is true
> - Function must receive `callback` as first argument.
> - To return list of rows/items for table, it must invoke callback function with object as parameter having following keys

<br>

| Keys   | Data Type        | Purpose                                                                                                                                                                                                                                                             |
| ------ | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| status | Number           | 1. Pass value as `200` - which indicates success and then table will retrieve `msg` key and loop it over to display items in table <br> 2. Pass value other than `200` - which indicates there is some error and table will alert the error message from `msg` key. |
| msg    | Array Of Objects | Each Object must contain all the keys defined in `key` property in [fields](#fields_attributes) and respective value.                                                                                                                                               |

<br>

**<h2 id="load_entries_attributes">loadEntries : Function</h2>**

> - This is the first function which will be called when data-vue-table loads.
> - This function will be called if [offLineMode](#offline_mode_attributes) is false or [offLineMode](#offline_mode_attributes) has not been passed
> - Function must receive `start`,`recordsPerPage`,`currentSort`,`currentSortDir`,`searchText`,`defaultSearchColumns`,`hideLoading`,`callback` as arguments.
> - In this function you can call your API to get the table data based on above `arguments`.
> - This function will be called every time when user changes any property For Ex: Sorting, Searching, Pagination.
> - To return list of rows/items for table, it must invoke callback function with object as parameter having following keys.

<br>

| Keys   | Data Type        | Purpose                                                                                                                                                                                                                                                             |
| ------ | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| status | Number           | 1. Pass value as `200` - which indicates success and then table will retrieve `msg` key and loop it over to display items in table <br> 2. Pass value other than `200` - which indicates there is some error and table will alert the error message from `msg` key. |
| msg    | Array Of Objects | Each Object must contain all the keys defined in `key` property in [fields](#fields_attributes) and respective value.                                                                                                                                               |
| count  | Number           | Total number of overall records present in database based on which the pagination will work.                                                                                                                                                                        |

<br>

**<h2 id="default_sort_attributes">defaultSort: String</h2>**

> - Must be passed as props
> - Value should match one of the [fields'](#fields_attributes) key

<br>

**<h2 id="default_sort_dir_attributes">defaultSortDir: String</h2>**

> Must be passed as props

| Value | Purpose                                                                    |
| ----- | -------------------------------------------------------------------------- |
| asc   | To sort [defaultSort](#default_sort_attributes) column in Ascending Order.  |
| desc  | To sort [defaultSort](#default_sort_attributes) column in Descending Order. |

<br>

**<h2 id="actions_attributes">actions: String</h2>**

> This prop will make **Action** column visible/hidden.

| Value | Purpose                                                                                                |
| ----- | ------------------------------------------------------------------------------------------------------ |
| true  | This will make **Action** column visible.<br>You must have to use [actionList](#action_list_attributes) |
| false | This will make **Action** column hidden.                                                               |

<br>

**<h2 id="fixed_action_column_on_left_attributes">fixedActionColumnOnLeft: Boolean</h2>**

> - This prop is only valid if you have opted for [actions](#actions_attributes).
> - This prop will move **Action** column as `first column` of the table.
> - This also makes the **Action** column as fixed and non scrollable.
> - This prop is `not mandatory` > `By default`, the **Action** column will be displayed as the `last column` of the table.

| Value | Purpose                                                             |
| ----- | ------------------------------------------------------------------- |
| true  | This prop will move **Action** column as first column of the table. |
| false | This prop will move **Action** column as last column of the table.  |

<br>

**<h2 id="action_list_attributes">actionList : Array of Objects</h2>**

> - This prop is only valid if you have opted for [actions](#actions_attributes).
> - This will generate the `Action Button(s)` for each row.
> - Each object should contain appropriate keys mentioned below

| Properties | Data Type | Mandatory | Possible Options | Purpose                                                                                                                                                                                                                                                                                                                                |
| ---------- | --------- | --------- | ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type       | String    | Yes       | link,cb          | This will define the type of `action button` <br>1. `link` -> The button will be treated as navigational link and then you also have to define `refAddress` key as defined below.<br>2. `cb` -> When button is clicked then `refAddress` function will be called.                                                                      |
| refAddress | Function  | Yes       | NA               | The function should receive `argument` which will contain single row data.<br>1. Incase of `link` type -> this should `return` URL which will be placed in `<a href="">` <br>2. Incase of `cb`, you can write any custom code inside function as per your need.                                                                        |
| getIcon    | Function  | Yes       | NA               | Function should receive `argument` which will contain single row data and it should return <br> 1. If `html` property mentioned below is 'true' then return html content which will render as icon.<br>2. If `html` property mentioned below is 'false' then return any [Materialize Icon Name](https://materializecss.com/icons.html) |
| html       | String    | Yes       | true,false       | You can customize your icon with this property. If value is `true` then `getIcon` should return html content or else should return any [Materialize Icon Name](https://materializecss.com/icons.html)                                                                                                                                  |
| hoverTitle | String    | No        | ANY              | This text would be visible when user will hover on icon.                                                                                                                                                                                                                                                                               |

**<h2 id="default_search_columns_attributes">defaultSearchColumns: Array of Strings</h2>**

> - This will allow `Global Search` box to search on specified columns only.
> - This will only work when [hideSearchBox](#hide_search_box_attributes) is `false` or [hideSearchBox](#hide_search_box_attributes) is not passed.
> - Array must contain String elements and each element should match one of [fields'](#fields_attributes) key.

<br>

**<h2 id="show_search_filter_attributes">showSearchFilter: Boolean</h2>**

> - This will allow `Global Search` box to search on user selected columns.
> - By default the `Global Search` box will search based on [defaultSearchColumns](#default_search_columns_attributes).
> - This will only work when [hideSearchBox](#hide_search_box_attributes) is `false` or [hideSearchBox](#hide_search_box_attributes) is not passed.

<br>

**<h2 id="search_by_filter_name_attributes">searchByFilterName: String</h2>**

> - This will allow to change the title of `Search Filter` popup and this is Optional.
> - `By default` the title will be **"Search By"**.
> - This will only work when [showSearchFilter](#show_search_filter_attributes) is `true`.
> - This will only work when [hideSearchBox](#hide_search_box_attributes) is `false` or [hideSearchBox](#hide_search_box_attributes) is not passed.

<br>

**<h2 id="show_search_filter_notification_attributes">showSearchFilterNotification: Boolean</h2>**

> - This will show `Count` of columns selected for search filter and this is Optional.
> - `By default` the notification will not be shown.
> - This will only work when [showSearchFilter](#show_search_filter_attributes) is `true`.
> - This will only work when [hideSearchBox](#hide_search_box_attributes) is `false` or [hideSearchBox](#hide_search_box_attributes) is not passed.

<br>

**<h2 id="fixed_search_box_text_attributes">fixedSearchBoxText: Boolean</h2>**

> - This will fix the default text of `Global Search Box`.
> - `By default` the text will be generated based on searchable columns.
> - This will only work when [showSearchFilter](#show_search_filter_attributes) is `true`.
> - This will only work when [hideSearchBox](#hide_search_box_attributes) is `false` or [hideSearchBox](#hide_search_box_attributes) is not passed.

<br>

**<h2 id="show_column_filter_attributes">showColumnFilter: Boolean</h2>**

> - This will allow user to `Show/Hide` selected columns.
> - By default all the columns are visible.

<br>

**<h2 id="column_filter_name_attributes">columnFilterName: String</h2>**

> - This will allow to change the title of `Column Filter` popup and this is Optional.
> - `By default` the title will be **"View By"**.
> - This will only work when [showColumnFilter](#show_column_filter_attributes) is `true`.

<br>

**<h2 id="show_column_filter_notification_attributes">showColumnFilterNotification: Boolean</h2>**

> - This will show `Count` of columns selected for search filter and this is Optional.
> - `By default` the notification will not be shown.
> - This will only work when [showColumnFilter](#show_column_filter_attributes) is `true`.

<br>

**<h2 id="export_excel_attributes">exportExcel: Boolean</h2>**

> - This option will provide a `download` button option on top right.
> - Upon clicking on button - there will be two options shown<br>1. `All Data` -> This will export all the rows without any filter<br>2. `Only Filtered` -> This will download only filtered rows
> - This will only work when [offLineMode](#offline_mode_attributes) is `true`.

<br>

**<h2 id="moveable_column_attributes">moveableColumn: Boolean</h2>**

> This option will allow the column's header to be draggable so that order of the columns can be rearraged.

<br>

**<h2 id="show_column_filter_button_attributes">showColumnFilterButton: Boolean</h2>**

> - This option will allow user to filter on individual columns.
> - This option will provide a `Filter` button option on top right.
> - Upon clicking on this button will toggle `column filter options` on each column header.
> - This will work on only those columns (Object) of [fields](#fields_attributes) which contains `multiFilterOption` as true.

<br>

**<h2 id="show_lock_columns_button_attributes">showLockColumnsButton: Boolean</h2>**

> - This option will allow user to `lock/pin` individual columns.
> - This option will provide a `Lock` button option on top right.
> - Upon clicking on this button will toggle `column lock/pin options` on each column header.
> - This will work on only those columns (Object) of [fields](#fields_attributes) which contains `lockable` as true.


<br>

**<h2 id="memorize_settings_locally_attributes">memorizeSettingsLocally: Boolean</h2>**

> - This option will automatically memorize all the user changes locally which will be applied when browser is refreshed or visited next time.
> - This option will also provide a `clear saved` button option on top right.
> - Upon clicking on this button will clear all the locally stored settings.
> - Button will be colored if something is stored locally, whereas it will be greyed when there is no data saved.

<br>


---



# **<h1 id="custom_buttons">Custom buttons on header</h1>**

> - data-table-vue provides the facility to add your own custom buttons on header section.
> - There are two slots where custom buttons can be placed<br>1. Left side on the header<br>2. Right side on the header.

**<h2 id="add_custom_buttons_left_attributes">1. Add custom buttons on left side</h2>**

> - Pass your html code inside the `data-table-vue directive`.
> - Use slot name as `headerOptionsLeft`.
> - `Sample code` is shown below

#### **Template Section**

```html
<template>
 <div>
   <div class="col s12">
     <div class="card">
       <div class="card-content">
         <div class="row no-margin">
           <div id="viewAll" class="col s12">
             <div class="row no-margin">
               <div class="col s12">
                 <Table :offLineMode="true" :fields="tableComponentData.fields"
                    :loadOfflineEntries="loadOfflineEntries" defaultSort="id" defaultSortDir="asc"
                    tableUniqueId="test_table" :perPageOptions="tableComponentData.perPageOptions"
                    :hideSearchBox="false" :noPagination="false" tableTitle="Test Table" actions="true"
                    :actionList="tableComponentData.actionList" :defaultSearchColumns="['id', 'name']"
                    :showSearchFilter="true" searchByFilterName="This is Filter Title"
                    :showSearchFilterNotification="true" :showColumnFilter="true"
                    columnFilterName="This is column show/hide options" :showColumnFilterNotification="true"
                    :columnFilters="false" :exportExcel="true" :moveableColumn="true" :showColumnFilterButton="true"
                    :showLockColumnsButton="true" :memorizeSettingsLocally="true">
                    <template v-slot:headerOptionsLeft>
                      <button class="btn-flat grey lighten-4 red-text minorMargin" @click="callAnyCustomLocalFunction()">
                        <i class="material-icons">assessment</i>
                      </button>
                    </template>
                  </Table>
               </div>
             </div>
           </div>
         </div>
       </div>
     </div>
   </div>
 </div>
</template>
```


## Screenshot - With custom button on left side

![Custom buttons on left side](https://github.com/Rahul6424/data-table-vue/blob/master/public/Step-15.png?raw=true "Custom buttons on left side")

<br>

**<h2 id="add_custom_buttons_right_attributes">2. Add custom buttons on right side</h2>**

> - Pass your html code inside the `data-table-vue directive`.
> - Use slot name as `headerOptionsRight`.
> - `Sample code` is shown below

#### **Template Section**

```html
<template>
 <div>
   <div class="col s12">
     <div class="card">
       <div class="card-content">
         <div class="row no-margin">
           <div id="viewAll" class="col s12">
             <div class="row no-margin">
               <div class="col s12">
                 <Table :offLineMode="true" :fields="tableComponentData.fields"
                    :loadOfflineEntries="loadOfflineEntries" defaultSort="id" defaultSortDir="asc"
                    tableUniqueId="test_table" :perPageOptions="tableComponentData.perPageOptions"
                    :hideSearchBox="false" :noPagination="false" tableTitle="Test Table" actions="true"
                    :actionList="tableComponentData.actionList" :defaultSearchColumns="['id', 'name']"
                    :showSearchFilter="true" searchByFilterName="This is Filter Title"
                    :showSearchFilterNotification="true" :showColumnFilter="true"
                    columnFilterName="This is column show/hide options" :showColumnFilterNotification="true"
                    :columnFilters="false" :exportExcel="true" :moveableColumn="true" :showColumnFilterButton="true"
                    :showLockColumnsButton="true" :memorizeSettingsLocally="true">
                    <template v-slot:headerOptionsRight>
                      <button class="btn-flat grey lighten-4 red-text minorMargin"
                        @click="callAnyCustomLocalFunction()">
                        <i class="material-icons">add_box</i>
                      </button>
                    </template>
                    <template v-slot:headerOptionsLeft>
                      <button class="btn-flat grey lighten-4 red-text minorMargin"
                        @click="callAnyCustomLocalFunction()">
                        <i class="material-icons">assessment</i>
                      </button>
                    </template>
                  </Table>
               </div>
             </div>
           </div>
         </div>
       </div>
     </div>
   </div>
 </div>
</template>
```


## Screenshot - With custom button on right side

![Custom buttons on right side](https://github.com/Rahul6424/data-table-vue/blob/master/public/Step-16.png?raw=true "Custom buttons on right side")

<br>