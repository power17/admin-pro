<template>
    <div>
        <el-tree
            ref="treeRef"
            :data="authList"
            :check-strictly="true"
            show-checkbox
            :default-checked-keys="checkedNode"
            node-key="roleId"
            :props="{ label: 'name', children: 'roleList' }"
        />
        <el-button type="primary" @click="onChangeAuth">修改权限</el-button>
    </div>
</template>
<script lang="ts" setup>
import { ref, onMounted } from 'vue';
import { LocationQueryValue, useRoute } from 'vue-router';
import { getAuthList } from '@/api/auth';
const route = useRoute();
interface IAuth {
    name: string; // 权限名称
    roleId: number; // 角色ID
    roleList?: IAuth[]; // 角色列表 子权限
}
const treeRef = ref<any>(null);
let authList = ref<IAuth[]>([]);
const checkedNode = ref<number[]>([]);
const { query } = route;
const auth = Array.isArray(query.auth) && query.auth.map((value: LocationQueryValue) => Number(value));
if (auth) {
    checkedNode.value = auth;
}
onMounted(() => {
    getAuthList({})
        .then((res) => {
            authList.value = res.data;
        })
        .catch((err) => {});
});
const onChangeAuth = () => {
    console.log(treeRef.value);
    const selectedTreeNode = treeRef.value.getCheckedNodes();
    console.log(selectedTreeNode);
    console.log(treeRef.value.getCheckedKeys());
};
</script>
