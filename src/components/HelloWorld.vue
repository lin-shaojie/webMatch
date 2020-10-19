<template>
  <div>
    <el-tabs type="border-card">
      <el-tab-pane label="我的订单">我的订单</el-tab-pane>
      <el-tab-pane label="常用联系人">
        <el-card class="box-card">
          <div slot="header" class="clearfix" style="text-align: center">
            <span style="float: left">常用联系人</span>
          </div>
          <el-table :data="tableData" style="width: 100%" ref="tables">
            <el-table-column label="默认联系人" width="200">
              <template>
                <el-radio v-model="radio"></el-radio>
              </template>
            </el-table-column>
            <el-table-column label="联系人姓名" width="180" prop="name">
            </el-table-column>

            <el-table-column label="联系人电话" width="200" prop="phone">
            </el-table-column>

            <el-table-column label="联系人地址" width="300">
              <template slot-scope="scope">
                <p>{{ scope.row.address }}</p>
              </template>
            </el-table-column>

            <el-table-column label="操作">
              <template slot-scope="scope">
                <el-button
                  size="mini"
                  @click="handleEdit(scope.$index, scope.row)"
                  >编辑</el-button
                >
                <el-button
                  size="mini"
                  @click="handleDelete(scope.$index, scope.row)"
                  >删除</el-button
                >
              </template>
            </el-table-column>
          </el-table>
        </el-card>

        <el-form
          :label-position="labelPosition"
          label-width="80px"
          :model="formLabelAlign"
          style="margin-top: 50px"
        >
          <el-row :gutter="20">
            <el-col :span="12">
              <el-form-item label="姓名*" style="vertical-align: top">
                <el-input v-model="formLabelAlign.name"></el-input>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item label="电话*">
                <el-input v-model="formLabelAlign.region"></el-input>
              </el-form-item>
            </el-col>
          </el-row>

          <el-row>
            <el-col :span="24">
              <el-form-item label="地址*">
                <el-input v-model="formLabelAlign.type"></el-input>
              </el-form-item>
            </el-col>
          </el-row>
        </el-form>

        <el-row type="flex" class="row-bg" justify="end">
          <el-col :span="3"
            ><el-button type="success" @click="addPeople"
              >保存联系人</el-button
            ></el-col
          >
        </el-row>
      </el-tab-pane>

      <el-tab-pane label="我的收藏">我的收藏</el-tab-pane>
      <el-tab-pane label="个人设置">个人设置</el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      tableData: [
        {
          date: "2016-05-02",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1518 弄",
          phone: "123",
        },
        {
          date: "2016-05-04",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1517 弄",
          phone: "465",
        },
        {
          date: "2016-05-01",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1519 弄",
          phone: "789",
        },
        {
          date: "2016-05-03",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1516 弄",
        },
      ],
      radio: "1",
      formLabelAlign: {
        name: "",
        region: "",
        type: "",
      },
      labelPosition: "top",
    };
  },
  methods: {
    handleEdit(index, row) {
      console.log(index, row);
    },
    handleDelete(index, row) {
      console.log(index, row);
    },
    addPeople() {
      this.tableData.push(this.formLabelAlign)
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.clearfix:before,
.clearfix:after {
  display: table;
  content: "";
}
.clearfix:after {
  clear: both;
}
</style>
