<template>
  <div>
    <el-container class="home">
      <el-aside class="aside">
        <!-- 菜单 -->
        <el-row class="tac">
          <el-col>
            <el-menu
              router
              default-active="2"
              class="el-menu-vertical-demo"
              @open="handleOpen"
              close="handleClose"
              background-color="rgb(48, 65, 86)"
              text-color="rgb(191, 203, 217)"
              :collapse="iscollapse"
            >
              <el-menu-item index="/home/index">
                <i class="el-icon-menu"></i>
                <span slot="title">首页</span>
              </el-menu-item>
              <el-menu-item index="/home/document">
                <i class="el-icon-menu"></i>
                <span slot="title">文档</span>
              </el-menu-item>
              <el-menu-item index="/home/lead">
                <i class="el-icon-menu"></i>
                <span slot="title">引导页</span>
              </el-menu-item>

              <!-- default-active:当前激活菜单的索引 -->
              <!-- open close submenu 展开和收起触发的事件 -->
              <!-- 二级菜单 -->
              <el-submenu index="4">
                <template slot="title">
                  <i class="el-icon-location"></i>
                  <span>权限测试页</span>
                </template>
                <el-menu-item index="4-1">页面权限</el-menu-item>
                <el-menu-item index="4-2">指令权限</el-menu-item>
                <el-menu-item index="4-3">角色权限</el-menu-item>
              </el-submenu>

              <el-submenu index="5">
                <template slot="title">
                  <i class="el-icon-location"></i>
                  <span>图标</span>
                </template>
              </el-submenu>

              <el-submenu index="6">
                <template slot="title">
                  <i class="el-icon-location"></i>
                  <span>权限测试页</span>
                </template>
                <el-menu-item index="6-1">页面权限</el-menu-item>
                <el-menu-item index="6-2">指令权限</el-menu-item>
                <el-menu-item index="6-3">角色权限</el-menu-item>
              </el-submenu>

              <el-submenu index="7">
                <template slot="title">
                  <i class="el-icon-location"></i>
                  <span>权限测试页</span>
                </template>
                <el-menu-item index="7-1">页面权限</el-menu-item>
                <el-menu-item index="7-2">指令权限</el-menu-item>
                <el-menu-item index="7-3">角色权限</el-menu-item>
              </el-submenu>

              <el-submenu index="8">
                <template slot="title">
                  <i class="el-icon-location"></i>
                  <span>权限测试页</span>
                </template>
                <el-menu-item index="8-1">页面权限</el-menu-item>
                <el-menu-item index="8-2">指令权限</el-menu-item>
                <el-menu-item index="8-3">角色权限</el-menu-item>
              </el-submenu>

              <el-submenu index="9">
                <template slot="title">
                  <i class="el-icon-location"></i>
                  <span>权限测试页</span>
                </template>
                <el-menu-item index="9-1">页面权限</el-menu-item>
                <el-menu-item index="9-2">指令权限</el-menu-item>
                <el-menu-item index="9-3">角色权限</el-menu-item>
              </el-submenu>

              <el-submenu index="10">
                <template slot="title">
                  <i class="el-icon-location"></i>
                  <span>综合实力</span>
                </template>
                <el-menu-item index="10-1">页面权限</el-menu-item>
                <el-menu-item index="10-2">指令权限</el-menu-item>
                <el-menu-item index="10-3">角色权限</el-menu-item>
              </el-submenu>
             
            </el-menu>
          </el-col>
        </el-row>
      </el-aside>
      <!-- 路由 -->
      <router-view>
        <el-container>
     
        </el-container>
      </router-view>
    </el-container>
  </div>
</template>

<script>
import instance from "@/api/api";
export default {
  name: "HomeView",
  data() {
    return {
      iscollapse: false, //aside是否折叠
    };
  },
  created() {
    instance.get("/aa").then((res) => console.log(res));
  },
  methods: {
    handleOpen(key, keyPath) {
      console.log(key, keyPath);
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath);
    },
  },
};
</script>

<style lang="scss" scoped>
.home {
  .aside {
    margin: 0;
    padding: 0;
    .el-menu-vertical-demo {
      height: 100vh;
      .el-menu-item:hover,.el-submenu_title:hover{
        background: #303133 !important;;
      }
      
    }
  }
}
</style>