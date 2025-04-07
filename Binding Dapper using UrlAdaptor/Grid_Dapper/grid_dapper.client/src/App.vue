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
<script setup>
  import { provide } from "vue";
  import { GridComponent as EjsGrid, ColumnDirective as EColumn, ColumnsDirective as EColumns, Toolbar, Filter, Sort, Group, Page, Edit } from "@syncfusion/ej2-vue-grids";
  import { DataManager, UrlAdaptor } from "@syncfusion/ej2-data";
  const data = new DataManager({
    url: 'https://localhost:7230/api/Grid',
    insertUrl: 'https://localhost:7230/api/Grid/Insert',
    updateUrl: 'https://localhost:7230/api/Grid/Update',
    removeUrl: 'https://localhost:7230/api/Grid/Remove',
    // Enable batch URL when batch editing is enabled.
    //batchUrl: 'https://localhost:xxxx/api/Grid/BatchUpdate',
    adaptor: new UrlAdaptor(),
  });
  const editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true };
  const toolbar = ['Add', 'Edit', 'Delete', 'Update', 'Cancel', 'Search'];
  const customerIDRules = { required: true };
  const employeeIDRules = { required: true, number: true };
  const freightRules = { required: true, min: 1, max: 1000 };
  const shipCityRules = { required: true };
  provide('grid', [Toolbar, Filter, Sort, Group, Page, Edit]);
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
