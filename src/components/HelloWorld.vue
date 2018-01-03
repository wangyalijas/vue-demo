<template>
  <div class="hello" style="display: flex">
    <div style="flex: 3">
      <el-tree
        :data="data2"
        show-checkbox
        node-key="id"
        :default-expanded-keys="[2, 3]"
        :default-checked-keys="[5]"
        @node-click="currentChange"
        :props="defaultProps">
      </el-tree>
    </div>

    <div style="flex: 9">
      <el-table
        :data="tableData"
        stripe
        style="width: 100%">
        <el-table-column
          prop="id"
          label="序号"
          width="180">
        </el-table-column>
        <el-table-column
          prop="parentLabel"
          label="父机构名称"
          width="180">
        </el-table-column>
        <el-table-column
          prop="label"
          align="center"
          label="名称">
        </el-table-column>
      </el-table>
    </div>

  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      tableData:[],
      data2: [{
        id: 1,
        label: '一级 1',
        parentName: '',
        children: [{
          id: 4,
          label: '二级 1-1',
          parentName: '1',
          children: [{
            id: 9,
            label: '三级 1-1-1',
            parentName: '4',
          }, {
            id: 10,
            label: '三级 1-1-2',
            parentName: '4',
          }]
        }]
      }, {
        id: 2,
        label: '一级 2',
        parentName: '',
        children: [{
          id: 5,
          label: '二级 2-1',
          parentName: '2',
          children: [{
            id: 9,
            label: '三级 3-1',
            parentName: '5',
          }, {
            id: 10,
            label: '三级 3-2',
            parentName: '5',
          }]
        }, {
          id: 6,
          label: '二级 2-2',
          parentName: '2',
        }]
      }, {
        id: 3,
        label: '一级 3',
        parentName: '',
        children: [{
          id: 7,
          label: '二级 3-1',
          parentName: '3',
        }, {
          id: 8,
          label: '二级 3-2',
          parentName: '3',
        }]
      }],
      defaultProps: {
        children: 'children',
        label: 'label',
      }
    }
  },
  watch: {
    tableData: function (value) {
//      console.log(value);
    }
  },
  methods: {
    currentChange (self,node) {
      let tableData;
      let appendData;
      if (self.hasOwnProperty('children')) {
        tableData = self.children;
        appendData = {
          parentLabel: self.label
        }
      } else {
        tableData = [self];
        appendData = {
          parentLabel: node.parent.data.label
        };
      }

      this.appendDataToArrayItem(tableData, appendData);


      this.tableData = tableData
    },
    appendDataToArrayItem(array, data) {
      array.forEach(item => {
        Object.assign(item, data);
      });
    }
  }
}
</script>

<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
