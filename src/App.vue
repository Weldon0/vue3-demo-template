<script setup>
import axios from "axios";
import { ref } from "vue";

const list = ref([]);

// 请求数据填充列表

const getList = async () => {
  const res = await axios.get("/list");
  console.log(res.data);
  list.value = res.data;
};

getList();

const del = async (id) => {
  await axios.delete("/del", { params: { id } }); // ?name=23
  getList();
};
</script>

<template>
  <div class="app">
    <el-table :data="list">
      <el-table-column prop="id" label="ID"></el-table-column>
      <el-table-column prop="name" label="姓名" width="150"></el-table-column>
      <el-table-column prop="place" label="籍贯"></el-table-column>
      <el-table-column label="操作" width="100">
        <template #default="{ row }">
          <el-popconfirm title="是否删除" @confirm="del(row.id)">
            <template #reference>
              <el-button>Delete</el-button>
            </template>
          </el-popconfirm>
          <!-- <el-button type="primary" @click="del(row.id)" link>删除</el-button> -->
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>
<style>
.app {
  width: 980px;
  margin: 100px auto 0;
}
</style>
