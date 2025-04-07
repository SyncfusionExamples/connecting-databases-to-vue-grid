<template>
    <div id="app">
        <ejs-grid :dataSource='data' :allowPaging='true' :allowGrouping='true' :allowFiltering='true' :allowSorting='true' :editSettings='editSettings' :toolbar='toolbar' height="348">
            <e-columns>
                <e-column field='OrderID' headerText='Order ID' width='100' textAlign='Right' isPrimaryKey='true' isIdentity='true'></e-column>
                <e-column field='CustomerID' headerText='Customer Name' :validationRules='customerIDRules' width='100'></e-column>
                <e-column field='EmployeeID' headerText='Employee ID' :validationRules='employeeIDRules' textAlign='Right' width='100'></e-column>
                <e-column field='Freight' headerText='Freight' :validationRules='freightRules' format='C2' textAlign='Right' width='100'></e-column>
                <e-column field='ShipCity' headerText='Ship City' :validationRules='shipCityRules' width='120'></e-column>
            </e-columns>
        </ejs-grid>
    </div>
</template>

<script>
  import { GridComponent, ColumnsDirective, ColumnDirective, Toolbar, Filter, Sort, Group, Page, Edit } from '@syncfusion/ej2-vue-grids';
  import { DataManager, UrlAdaptor } from '@syncfusion/ej2-data';
  export default {
    name: "App",
    components: {
      'ejs-grid': GridComponent,
      'e-columns': ColumnsDirective,
      'e-column': ColumnDirective
    },
    data() {
      return {
        data: new DataManager({
          url: 'https://localhost:xxxx/api/Grid',
          insertUrl: 'https://localhost:xxxx/api/Grid/Insert',
          updateUrl: 'https://localhost:xxxx/api/Grid/Update',
          removeUrl: 'https://localhost:xxxx/api/Grid/Remove',
          // Enable batch URL when batch editing is enabled.
          //batchUrl: 'https://localhost:xxxx/api/Grid/BatchUpdate',
          adaptor: new UrlAdaptor(),
        }),
        editSettings: { allowAdding: true, allowDeleting: true, allowEditing: true},
        toolbar: ['Add', 'Edit', 'Delete', 'Update', 'Cancel', 'Search'],
        customerIDRules: { required: true },
        employeeIDRules: { required: true, number: true },
        freightRules: { required: true, min: 1, max: 1000 },
        shipCityRules: { required: true },
      };
    },
    provide: {
      grid: [Toolbar, Filter, Sort, Group, Page, Edit]
    }
  };
</script>

<style>
    @import "../node_modules/@syncfusion/ej2-base/styles/tailwind.css";
    @import "../node_modules/@syncfusion/ej2-buttons/styles/tailwind.css";
    @import "../node_modules/@syncfusion/ej2-calendars/styles/tailwind.css";
    @import "../node_modules/@syncfusion/ej2-dropdowns/styles/tailwind.css";
    @import "../node_modules/@syncfusion/ej2-inputs/styles/tailwind.css";
    @import "../node_modules/@syncfusion/ej2-navigations/styles/tailwind.css";
    @import "../node_modules/@syncfusion/ej2-popups/styles/tailwind.css";
    @import "../node_modules/@syncfusion/ej2-splitbuttons/styles/tailwind.css";
    @import "../node_modules/@syncfusion/ej2-vue-grids/styles/tailwind.css";
</style>

