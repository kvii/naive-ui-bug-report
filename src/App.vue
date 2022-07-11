<script setup lang="ts">
import { NTree, TreeOption } from "naive-ui";
import { Ref, ref } from 'vue';

/** 当前选中的 key */
const checkedKeys: Ref<string[]> = ref([])

/** 树形选择数据 */
const data: Ref<TreeOption[]> = ref(<TreeOption[]>[
    {
        key: 1,
        label: '第一步：点击左边的 checkbox',
        children: <TreeOption[]>[
            { key: 2, label: '2', isLeaf: true },
            { key: 3, label: '3', isLeaf: true },
        ],
    },
])

let currentInnerKey = 3;

/** 在组件外添加一条子数据 */
function insert() {
    currentInnerKey++;
    const value: TreeOption = {
        key: currentInnerKey,
        label: `${currentInnerKey} <- 在组件外添加的数据`,
        isLeaf: true,
    }

    data.value[0].children!.push(value)
}
</script>

<template>
    <section class="my-container">
        <code>checkedKeys: {{ checkedKeys }}</code>

        <NTree
            checkable
            cascade
            :data="data"
            :default-expand-all="true"
            v-model:checked-keys="checkedKeys" />

        <button @click="insert">第二步：点击按钮，添加一条子数据</button>

        <span>期望结果：<code>checkedKeys: [ 1, 2, 3, 4 ]</code></span>

        <div>
            <h1>说明</h1>
            当用户在组件外向 data 添加数据时，<br />
            字段 checked-keys 的值应该与 checkbox 的实际状态一致。<br />
        </div>
    </section>
</template>

<style>
.my-container {
    width: 400px;
    padding: 24px;
    margin: auto;
    display: flex;
    flex-direction: column;
}
</style>