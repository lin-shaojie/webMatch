<template>
    <el-tabs type="border-card">
      <el-tab-pane label="我的订单">我的订单</el-tab-pane>
      <el-tab-pane label="常用联系人">
        <el-card class="box-card">
          <div slot="header" class="clearfix" >
            <span>常用联系人</span>
          </div>
          <el-table :data="tableData" style="width: 100%" ref="tables">
            <el-table-column label="默认联系人" width="200">
              <template slot-scope="scope">
                <el-radio
                  v-model="radio"
                  :label="scope.$index"
                  @change="getCurrentRow(scope.$index)"
                  >{{ &nbsp; }}</el-radio
                >
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
          label-position="top"
          label-width="80px"
          :model="formLabelAlign"
          style="margin-top: 50px"
        >
          <el-row :gutter="20">
            <el-col :span="12">
              <el-form-item label="姓名*">
                <el-input v-model="formLabelAlign.name"></el-input>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item label="电话*">
                <el-input v-model="formLabelAlign.phone"></el-input>
              </el-form-item>
            </el-col>
          </el-row>

          <el-row>
            <el-col :span="24">
              <el-form-item label="地址*">
                <el-input v-model="formLabelAlign.address"></el-input>
              </el-form-item>
            </el-col>
          </el-row>
        </el-form>

        <el-row type="flex" justify="end">
          <el-col :span="3"
            ><el-button type="success" @click="addPeople"
              >保存联系人</el-button
            ></el-col
          >
        </el-row>

        <el-dialog title="编辑地址" :visible.sync="dialogFormVisible">
          <el-form :model="formLabelAlign">
            <el-form-item label="姓名" :label-width="formLabelWidth">
              <el-input v-model="formLabelAlign.name" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="手机" :label-width="formLabelWidth">
              <el-input v-model="formLabelAlign.phone" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="地址" :label-width="formLabelWidth">
              <el-input v-model="formLabelAlign.address" autocomplete="off"></el-input>
            </el-form-item>
          </el-form>
          <div slot="footer" class="dialog-footer">
            <el-button @click="dialogFormVisible = false">取 消</el-button>
            <el-button type="primary" @click="dialogFormVisible = false"
              >确 定</el-button
            >
          </div>
        </el-dialog>
      </el-tab-pane>

      <el-tab-pane label="我的收藏">我的收藏</el-tab-pane>
      <el-tab-pane label="个人设置">个人设置</el-tab-pane>
    </el-tabs>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      tableData: [
        {
          name: "王小虎",
          address: "上海市普陀区金沙江路 1518 弄",
          phone: "123",
        },
        {
          name: "王小虎",
          address: "上海市普陀区金沙江路 1517 弄",
          phone: "465",
        },
        {
          name: "王小虎",
          address: "上海市普陀区金沙江路 1519 弄",
          phone: "789",
        },
        {
          name: "王小虎",
          phone: "110",
          address: "上海市普陀区金沙江路 1516 弄",
        },
      ],
      radio: 1,
      formLabelAlign: {
        name: "",
        phone: "",
        address: "",
      },
      dialogFormVisible: false,
      formLabelWidth: '80px'
    };
  },
  methods: {
    handleEdit(index, row) {
      this.dialogFormVisible = true
      this.formLabelAlign = JSON.parse(JSON.stringify(this.tableData[index]))
      console.log(index, row);
    },
    handleDelete(index, row) {
      console.log(index, row);
      this.$confirm("此操作将永久删除该条地址，是否继续？", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning",
      })
        .then(() => {
          this.tableData.splice(index, 1);
          this.$message({
            type: "success",
            message: "删除成功!",
          });
        })
        .catch(() => {
          this.$message({
            type: "info",
            message: "已取消删除",
          });
        });
    },
    addPeople() {
      this.tableData.push(JSON.parse(JSON.stringify(this.formLabelAlign)));
    },
    getCurrentRow(row) {
      this.$confirm("此操作将永久删除该文件, 是否继续?", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning",
      })
        .then(() => {
          this.$message({
            type: "success",
            message: "删除成功!",
          });
          location.reload();
        })
        .catch(() => {
          this.$message({
            type: "info",
            message: "已取消删除",
          });
        });
    },
  },
};
</script>

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
