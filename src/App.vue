<template>
  <div id="app">
    <el-container>
        <el-header><h1>API Browser</h1></el-header>
        <hr />
        <el-main>
            <data-tables :data='tableData' :actions-def='getActionsDef()' :action-col-def="actionColDef" :checkbox-filter-def='getCheckFilterDef()'>
                <el-table-column prop="API" label="API" sortable="custom"></el-table-column>
                <el-table-column prop="Category" label="Category" sortable="custom"></el-table-column>
                <el-table-column prop="Description" label="Description" sortable="custom"></el-table-column>
                <el-table-column prop="Auth" label="Auth" sortable="custom"></el-table-column>
                <el-table-column prop="HTTPS" label="HTTPS" sortable="custom"></el-table-column>
            </data-tables>
        </el-main>
    </el-container>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      tableData: [],
      actionColDef: {
        label: "Link",
        def: [
          {
            handler: row => {
              window.open(row.Link);
            },
            name: "Go"
          }
        ]
      },
      paginationDef: {
        show: false,
        currentPage: 5
      }
    };
  },
  created: function() {
    var that = this;
    const jsonDataSourceURL =
      "https://raw.githubusercontent.com/toddmotto/public-apis/master/json/entries.min.json";
    // Use fetch API to grab json from git repo
    fetch(jsonDataSourceURL)
      .then(function(response) {
        // Convert to JSON
        return response.json();
      })
      .then(function(jsonData) {
        // Transform data to work with Data Tables
        jsonData.entries.map(function(row, index) {
          // Overwrite Auth with "None" if value is null
          if (row.Auth === null) {
            jsonData.entries[index].Auth = "None";
          }
          // Overwrite HTTPS true/false values to "Yes/No"
          jsonData.entries[index].HTTPS === true
            ? (jsonData.entries[index].HTTPS = "Yes")
            : (jsonData.entries[index].HTTPS = "No");
        });
        that.tableData = jsonData.entries;
      });
  },
  methods: {
    getActionsDef() {
      let self = this;
      return {
        width: 5,
        def: [
          {
            name: "Source Code",
            handler() {
              window.open('https://github.com/kschluter/api-browser');
            },
            icon: "plus"
          }
        ]
      };
    },
    getCheckFilterDef() {
      return {
        width: 14,
        props: "Auth",
        def: [
          {
            code: "apiKey",
            name: "apiKey"
          },
          {
            code: "OAuth",
            name: "OAuth"
          },
          {
            code: "X-Mashape-Key",
            name: "X-Mashape-Key"
          },
          {
            code: "None",
            name: "None"
          }
        ]
      };
    }
  }
};
</script>

<style>
body {
  font-family: Source Sans Pro,Helvetica Neue,Arial,sans-serif;
}
.el-header{
  height: 30px !important;
}
</style>
