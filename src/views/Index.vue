<template>
  <div>
    <h3>数据的增删改查</h3>
    <el-table :data="tableData" style="width: 100%">
      <el-table-column label="日期" prop="date" width="100px" align="center">
      </el-table-column>
      <el-table-column label="姓名" prop="name" width="100px" align="center">
      </el-table-column>
      <el-table-column label="地址" prop="address" width="400px" align="center">
        <template slot="header" slot-scope>
          <el-input v-model="search" size="mini" placeholder="输入关键字搜索" />
        </template>
      </el-table-column>
      <el-table-column label="修改" align="center" width="400px">
        <template slot-scope="scope">
          <el-button size="mini" @click="handleEdit(scope)">修改</el-button>
          <el-button size="mini" type="danger" @click="handleDelete(scope)"
            >删除</el-button
          >
        </template>
      </el-table-column>
    </el-table>
    <el-button @click="addfn">增加</el-button>
    <!-- 表单 -->
    <MyDialog
      :form="form"
      :dialogFormVisible="dialogFormVisible"
      :formLabelWidth="formLabelWidth"
      @confirmfn_my="confirmfn"
      @my_cancel="cancelfn"
    ></MyDialog>
    <!-- 增加弹窗 -->

    <!-- <div> -->
    <el-dialog title="添加新用户" :visible.sync="incrementform">
      <el-form :model="form">
        <el-form-item label="日期" :label-width="formLabelWidth">
          <el-date-picker
            v-model="form.date"
            type="date"
            placeholder="选择日期"
          >
          </el-date-picker>
        </el-form-item>
        <el-form-item label="姓名" :label-width="formLabelWidth">
          <el-input v-model="form.name" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="地址" :label-width="formLabelWidth">
          <el-input v-model="form.address" autocomplete="off"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="addcancelfn">取 消</el-button>
        <el-button type="primary" @click="confirmfn">确 定</el-button>
      </div>
    </el-dialog>
  </div>
</template>
<script>
import dayjs from "dayjs";
import instance from "../api/api";
import MyDialog from "../components/MyDialog.vue";
export default {
  name: "Index",
  data() {
    return {
      search: "",
      tableData: [],
      dialogFormVisible: false, //表单的显示隐藏
      form: {

        index: 0,
        date: null,
        name: "",
        address: "",
      }, //表单的内容
      formLabelWidth: "120px",
    };
  },
  components: {
    MyDialog,
  },
  created() {
    this.getall();
  },
  methods: {
    // 增加
    addfn() {},
    handleEdit(scope) {
      this.form = scope.row;
      this.form.index = scope.$index;
      this.dialogFormVisible = true;
    },
    handleDelete(scope) {
      console.log(scope);
      this.$confirm("确定删除吗", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning",
      })
        .then(() => {
          this.deletefn(scope.$index).then(() =>
            this.$message({
              type: "success",
              message: "删除成功!",
            })
          );
        })
        .catch(() => {
          this.$message({
            type: "info",
            message: "已取消删除",
          });
        });
    },
    confirmfn() {
      this.dialogFormVisible = false;
      this.form.date = dayjs(new Date(this.form.date)).format("YYYY-MM-DD");
      console.log(this.form.date);
      this.updatefn();
    },
    cancelfn() {
      this.dialogFormVisible = false;
    },
    // 增加
     async incrementfn() {
      // let {data,name,address,index} =this.addform
      // let {data} =await instance.post("/add",{

      // })
     },
    //修改业务
    async updatefn() {
      let { date, name, address, index } = this.form;
      let { data } = await instance.put("/update", {
        date,
        name,
        address,
        index,
      });
      console.log(data);
    },
    //删除业务
    async deletefn(index) {
      let { data } = await instance.delete("/delete", { params: { index } });
      console.log(data);
      this.getall();
    },
    //请求数据的业务
    async getall() {
      let { data } = await instance.get("/all");
      console.log(data);
      this.tableData = data.tabledata;
    },
  },
};
</script>
<style lang="sass" scoped>
</style>