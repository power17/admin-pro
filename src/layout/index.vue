<template>
    <el-container>
        <el-header>
            <Header></Header>
        </el-header>
        <el-container>
            <el-aside width="200px">
                <el-menu :default-active="activeMenu" :ellipsis="false" router>
                    <el-menu-item v-for="item in menuList" :key="item.path" :index="item.path">
                        <span>{{ item.meta.title }}</span>
                    </el-menu-item>
                </el-menu>
            </el-aside>
            <el-main>
                <router-view></router-view>
            </el-main>
        </el-container>
    </el-container>
</template>

<script lang="ts" setup>
import { useRouter, useRoute } from 'vue-router';
import Header from './components/Header.vue';
const router = useRouter();
const route = useRoute();
const menuList = router.getRoutes().filter((route) => {
    return route.meta.isShow;
});
const activeMenu = route.path;
</script>
<style scoped lang="less">
.el-header {
    padding: 0;
    margin-bottom: 5px;
}

.el-container {
    height: 100%;

    .el-menu {
        height: 100%;
    }
}
</style>
