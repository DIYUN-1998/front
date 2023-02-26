<template>
  <el-container style="min-height: 100vh">
    <el-aside :width="sideWidth + 'px'" style="background-color: rgb(238, 241, 246); box-shadow: 2px 0 6px rgb(0 21 41 / 35%);">
      <el-menu :default-openeds="['1', '3']" style="min-height: 100%; overflow-x: hidden"
               background-color="rgb(48, 65, 86)"
               text-color="#fff"
               active-text-color="#ffd04b"
               :collapse-transition="false"
               :collapse="isCollapse"
      >
        <div style="height: 60px; line-height: 60px; text-align: center">
          <img src="../assets/Fidelity-Logo.png" alt="" style="width: 50%; position: relative; top: 5px; margin-right: 5px">
          <b style="color: white" v-show="logoTextShow">Car Stack </b>
        </div>
        <el-submenu index="1">
          <template slot="title">
            <i class="el-icon-message"></i>
            <span slot="title">导航一</span>
          </template>
          <el-menu-item-group>
            <template slot="title">分组一</template>
            <el-menu-item index="1-1">选项1</el-menu-item>
            <el-menu-item index="1-2">选项2</el-menu-item>
          </el-menu-item-group>
          <el-menu-item-group title="分组2">
            <el-menu-item index="1-3">选项3</el-menu-item>
          </el-menu-item-group>
          <el-submenu index="1-4">
            <template slot="title">选项4</template>
            <el-menu-item index="1-4-1">选项4-1</el-menu-item>
          </el-submenu>
        </el-submenu>
        <el-submenu index="2">
          <template slot="title">
            <i class="el-icon-menu"></i>
            <span slot="title">导航二</span>
          </template>
          <el-menu-item-group>
            <template slot="title">分组一</template>
            <el-menu-item index="2-1">选项1</el-menu-item>
            <el-menu-item index="2-2">选项2</el-menu-item>
          </el-menu-item-group>
          <el-menu-item-group title="分组2">
            <el-menu-item index="2-3">选项3</el-menu-item>
          </el-menu-item-group>
          <el-submenu index="2-4">
            <template slot="title">选项4</template>
            <el-menu-item index="2-4-1">选项4-1</el-menu-item>
          </el-submenu>
        </el-submenu>
        <el-submenu index="3">
          <template slot="title">
            <i class="el-icon-setting"></i>
            <span slot="title">导航三</span>
          </template>
          <el-menu-item-group>
            <template slot="title">分组一</template>
            <el-menu-item index="3-1">选项1</el-menu-item>
            <el-menu-item index="3-2">选项2</el-menu-item>
          </el-menu-item-group>
          <el-menu-item-group title="分组2">
            <el-menu-item index="3-3">选项3</el-menu-item>
          </el-menu-item-group>
          <el-submenu index="3-4">
            <template slot="title">选项4</template>
            <el-menu-item index="3-4-1">选项4-1</el-menu-item>
          </el-submenu>
        </el-submenu>
      </el-menu>
    </el-aside>

    <el-container>

      <el-header style="font-size: 12px; border-bottom: 1px solid #ccc; line-height: 60px; display: flex">
        <div style="flex: 1; font-size: 20px">
          <span :class="collapseBtnClass"  @click="collapse"></span>
        </div>
        <el-dropdown style="width: 70px; cursor: pointer">
          <span>user</span><i class="el-icon-arrow-down" style="margin-left: 5px"></i>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item>person information</el-dropdown-item>
            <el-dropdown-item>log out</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>

      </el-header>

      <el-main>

        <div style="padding: 10px 0">
          <el-input style="width: auto;" suffix-icon="el-icon-search"></el-input><el-button class="ml-5" type="important">search</el-button>
        </div>

        <div style="margin: 10px 0">
          <el-button type="primary">add single column<i class="el-icon-circle-plus-outline"></i></el-button>
          <el-button type="danger">delete multiple columns <i class="el-icon-remove-outline"></i></el-button>
          <el-button type="primary">add multiple columns<i class="el-icon-bottom"></i></el-button>
          <el-button type="primary">export<i class="el-icon-top"></i></el-button>
        </div>

        <el-table :data="tableData" border stripe :header-cell-class-name="headerBg">
          <el-table-column prop="name" label="car name" width="auto" align="center">
          </el-table-column>
          <el-table-column prop="type" label="car type" width="auto" align="center">
          </el-table-column>
          <el-table-column prop="color" label="car color" align="center">
          </el-table-column>
          <el-table-column prop="factory" label="car color" align="center">
          </el-table-column>
          <el-table-column prop="local" label="car location" align="center">
          </el-table-column>
          <el-table-column label="Operation"  width="auto" align="center">
            <template slot-scope="scope">
              <el-button type="success" style="width: auto">Edit <i class="el-icon-edit"></i></el-button>
              <el-button type="danger">Delete <i class="el-icon-remove-outline"></i></el-button>
            </template>
          </el-table-column>
        </el-table>
        <div style="padding: 10px 0">
          <!--pagination中的-->
          <!--@size-change="handleSizeChange"-->
          <!--@current-change="handleCurrentChange"-->
          <!--:current-page="currentPage4"-->
          <el-pagination

            :page-sizes="[10, 20, 30, 40]"
            :page-size="100"
            layout="total, sizes, prev, pager, next, jumper"
            :total="400">
          </el-pagination>
        </div>
      </el-main>
    </el-container>
  </el-container>
</template>

<style>
  .el-header {
    background-color: #B3C0D1;
    color: #333;
    line-height: 60px;
  }

  .el-aside {
    color: #333;
  }
</style>
<script>
  export default {
    name: 'Home',
    data() {
      return {
        tableData: [],
        msg: "hello user",
        collapseBtnClass: 'el-icon-s-fold',
        isCollapse: false,
        sideWidth: 200,
        logoTextShow: true,
        headerBg:'headerBg'
      }
    },
    created(){
        //get whole table
      fetch("http://localhost:8888/carTable/wholeCar").then(allCarTable=> allCarTable.json()).then(allCarTable =>{
        console.log(allCarTable)
        this.tableData=allCarTable.data
      })

    },
    methods: {
      collapse() {  // when click collapse button
        this.isCollapse = !this.isCollapse
        if (this.isCollapse) {  // 收缩
          this.sideWidth = 64
          this.collapseBtnClass = 'el-icon-s-unfold'
          this.logoTextShow = false
        } else {   // 展开
          this.sideWidth = 200
          this.collapseBtnClass = 'el-icon-s-fold'
          this.logoTextShow = true
        }
      }
    }
  }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<!--<style scoped>-->
<!--h1, h2 {-->
  <!--font-weight: normal;-->
<!--}-->
<!--ul {-->
  <!--list-style-type: none;-->
  <!--padding: 0;-->
<!--}-->
<!--li {-->
  <!--display: inline-block;-->
  <!--margin: 0 10px;-->
<!--}-->
<!--a {-->
  <!--color: #42b983;-->
<!--}-->
<!--</style>-->
