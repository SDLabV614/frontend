<template>
  <el-menu
    class="el-menu-vertical-demo"
    :collapse="isCollapse"
    background-color="rgb(104 78 92)"
    text-color="#fff"
    active-text-color="#ffd04b"
  >
    <h4 style="color:#fff;text-align: center;line-height: 30px;font-weight:  bold" v-show="!isCollapse" >
      Sensor system</h4>
    <h3 v-show="isCollapse">backstage</h3>
    <el-menu-item
      :index="item.path"
      v-for="item in noChildren"
      :key="item.path"
      @click="clickMenu(item)"
    >
      <i :class="'el-icon-' + item.icon"></i>
      <span slot="title">{{ item.label }}</span>
    </el-menu-item>
    <el-submenu
      :index="item.label"
      v-for="item in hasChildren"
      :key="item.path"
    >
      <template slot="title">
        <i :class="'el-icon-' + item.icon"></i>
        <span slot="title">{{ item.label }}</span>
      </template>
      <el-menu-item-group>
        <el-menu-item
          :index="subItem.path"
          v-for="(subItem, subIndex) in item.children"
          :key="subIndex"
          @click="clickMenu(subItem)"
        >
          <i :class="'el-icon-' + subItem.icon"></i>
          <span slot="title">{{ subItem.label }}</span>
        </el-menu-item>
      </el-menu-item-group>
    </el-submenu>
  </el-menu>
</template>

<script>
export default {
  data() {
    return {
      menu: [
        {
          path: "/",
          name: "Home",
          label: "Home ",
          icon: "s-home",
          url: "Home/Home",
        },
        {
          // path: "/mall",
          name: "pattern",
          label: "pattern",
          icon: "video-play",
          url: "pattern/pattern",
        },
        
       
      ],
    };
  },
  methods: {
    // handleOpen(key, keyPath) {
    //   console.log(key, keyPath);
    // },
    // handleClose(key, keyPath) {
    //   console.log(key, keyPath);
    // },
    clickMenu(item) {
      console.log(item);
      this.$router.push({ name: item.name });
      this.$store.commit("selectMenu", item);
    },
  },
  computed: {
    noChildren() {
      return this.menu.filter((item) => !item.children);
    },
    hasChildren() {
      return this.menu.filter((item) => item.children);
    },
    isCollapse() {
      return this.$store.state.tab.isCollapse;
    },
  },
};
</script>

<style  scoped>
.el-menu {
  height: 100%;
  border: none;
}
.el-menu-vertical-demo:not(.el-menu--collapse) {
  width: 200px;
  min-height: 600px;
}
</style>



