<script>
  import { PivotViewComponent, GroupingBar, Toolbar, ConditionalFormatting } from "@syncfusion/ej2-vue-pivotview";
  import { createApp } from 'vue';
  const app = createApp();
  var templateVue = app.component("cellTemplate",{
    data()
    {
      return{
        data:{}
      };
    },
    methods:{
      getCellContent: function(e){
        var template;
        if(e && e.cellInfo && e.cellInfo.axis == 'value'){
          if(e.cellInfo.actualValue < 1000)
          {
            template = '<div class="icon-loss"></div>'
          }
          else if (e.cellInfo.actualValue > 1000 && e.cellInfo.actualValue < 5000) {
            template = '<div class=" icon-neutral "></div>';
          } else if (e.cellInfo.actualValue > 5000) {
            template = '<div class="icon-profit"></div>';
          }
          else{
            template=''
          }
        }
        else{
          template=''
        }
        return template;
      }
    },
    template: `<div v-if="getCellContent(data) !== ''">
              <div v-html="getCellContent(data)"></div>
            </div>`,
  });
  
export default{
  components: {
    "ejs-pivotview": PivotViewComponent
  },
  data()
  {
    return{
      dataSourceSettings:{
        dataSource:[
            { Amount: 5100, Country: "Canada", Date: "FY 2006", Quarter: "Q1", Product: "Car", Quantity: 21, State: "Alberta" },
            { Amount: 1900, Country: "France", Date: "FY 2007", Quarter: "Q2", Product: "Bike", Quantity: 23, State: "Alberta" },
            { Amount: 1000, Country: "Sweden", Date: "FY 2008", Quarter: "Q3", Product: "Car", Quantity: 29, State: "Alberta" },
            { Amount: 2060, Country: "Canada", Date: "FY 2006", Quarter: "Q4", Product: "Bike", Quantity: 93, State: "British Columbia" },
            { Amount: 6200, Country: "France", Date: "FY 2007", Quarter: "Q1", Product: "Car", Quantity: 36, State: "British Columbia" },
            { Amount: 2000, Country: "Sweden", Date: "FY 2008", Quarter: "Q2", Product: "Bike", Quantity: 31, State: "British Columbia" },
            { Amount: 1300, Country: "Canada", Date: "FY 2005", Quarter: "Q3", Product: "Car", Quantity: 45, State: "Brunswick" },
            { Amount: 3400, Country: "France", Date: "FY 2006", Quarter: "Q4", Product: "Bike", Quantity: 47, State: "Brunswick" },
            { Amount: 2300, Country: "Sweden", Date: "FY 2007", Quarter: "Q1", Product: "Car", Quantity: 43, State: "Brunswick" },
            { Amount: 5100, Country: "Canada", Date: "FY 2006", Quarter: "Q2", Product: "Bike", Quantity: 21, State: "Alberta" },
            { Amount: 1900, Country: "France", Date: "FY 2007", Quarter: "Q3", Product: "Car", Quantity: 23, State: "Alberta" },
            { Amount: 1000, Country: "Sweden", Date: "FY 2008", Quarter: "Q4", Product: "Bike", Quantity: 29, State: "Alberta" },
            { Amount: 2060, Country: "Canada", Date: "FY 2006", Quarter: "Q1", Product: "Car", Quantity: 93, State: "British Columbia" },
            { Amount: 6200, Country: "France", Date: "FY 2007", Quarter: "Q2", Product: "Bike", Quantity: 36, State: "British Columbia" },
            { Amount: 2000, Country: "Sweden", Date: "FY 2008", Quarter: "Q3", Product: "Car", Quantity: 31, State: "British Columbia" },
            { Amount: 1300, Country: "Canada", Date: "FY 2005", Quarter: "Q4", Product: "Bike", Quantity: 45, State: "Brunswick" },
            { Amount: 3400, Country: "France", Date: "FY 2006", Quarter: "Q1", Product: "Car", Quantity: 47, State: "Brunswick" },
            { Amount: 2300, Country: "Sweden", Date: "FY 2007", Quarter: "Q2", Product: "Bike", Quantity: 43, State: "Brunswick" },
       ],
        rows: [{name:'Country'},{name: 'Product'}],
        columns: [{name:'Date'}],
        values: [{name:'Amount'}, {name:'Quantity', caption:'Units Sold'}],
        formatSettings: [{name:'Amount', format:'C1'}],
        conditionalFormatSettings:[
          {
            
            value1:3000,
            conditions:'LessThan',
            style:{
              backgroundColor: '#80cbc4',
              color: 'black',
              fontFamily: 'Tahoma',
              fontSize: '12px'
            }
          }
        ]
      },
      height:'350px',
      width:'900px',
      showGroupingBar: true,
      showToolbar: true,
      allowConditionalFormatting: true,
      toolbar: ["ConditionalFormatting"],
      cellTemplate: function()
      {
        return{
          template: templateVue
        };
      }
  }},
  provide:
  {
    pivotview:[ GroupingBar, Toolbar, ConditionalFormatting ]
  }
}
</script>
<template>
  <ejs-pivotview :height="height" :width="width"
                 :dataSourceSettings="dataSourceSettings"
                 :showGroupingBar ="showGroupingBar"
                 :cellTemplate="cellTemplate"
                 :showToolbar="showToolbar"
                 :allowConditionalFormatting="allowConditionalFormatting"
                 :toolbar="toolbar"
                 ></ejs-pivotview>
</template>

<style >
  @import "../node_modules/@syncfusion/ej2-base/styles/bootstrap5.css";
  @import "../node_modules/@syncfusion/ej2-inputs/styles/bootstrap5.css";
  @import "../node_modules/@syncfusion/ej2-buttons/styles/bootstrap5.css";
  @import "../node_modules/@syncfusion/ej2-splitbuttons/styles/bootstrap5.css";
  @import "../node_modules/@syncfusion/ej2-calendars/styles/bootstrap5.css";
  @import "../node_modules/@syncfusion/ej2-dropdowns/styles/bootstrap5.css";
  @import "../node_modules/@syncfusion/ej2-lists/styles/bootstrap5.css";
  @import "../node_modules/@syncfusion/ej2-popups/styles/bootstrap5.css";
  @import "../node_modules/@syncfusion/ej2-navigations/styles/bootstrap5.css";
  @import "../node_modules/@syncfusion/ej2-grids/styles/bootstrap5.css";
  @import "../node_modules/@syncfusion/ej2-vue-pivotview/styles/bootstrap5.css";
  .icon-neutral {
        display: inline-block !important;
        width: 0;
        height: 0;
        border-top: 5px solid transparent;
        border-bottom: 5px solid transparent;
        border-left: 5px solid blue;
        margin-left: 10px;
      }
      .icon-loss {
        display: inline-block !important;
        width: 0;
        height: 0;
        border-left: 5px solid transparent;
        border-right: 5px solid transparent;
        border-top: 5px solid #f00;
        margin-left: 10px;
      }
      .icon-profit {
        display: inline-block !important;
        width: 0;
        height: 0;
        border-left: 5px solid transparent;
        border-right: 5px solid transparent;
        border-bottom: 5px solid darkgreen;
        margin-left: 10px;
      }
 </style>


