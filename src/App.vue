<template>
  <div id="app">
    <el-input v-model="a" placeholder="Please enter keyword" />
    <el-input
      v-model="query"
      placeholder="Please enter keyword"
      @input="onQueryChanged"
    />

    <el-tree-v2
      ref="treeRef"
      :data="data"
      :props="props"
      :filter-method="filterMethod"
      :height="208"
    />
  </div>
</template>

<script>
import { ref } from 'vue';
import { ElInput,ElTreeV2 } from 'element-plus';
import maplist from './components/map.json';

export default {
  name: 'App',
  components: {
    maplist,
    ElInput,
    ElTreeV2
  },
  setup() {

    interface Tree {
      id: string
      label: string
      children?: Tree[]
    }

    const a = ref('as');

    const query = ref('')
    const treeRef = ref<InstanceType<typeof ElTreeV2>>()
    const data = maplist
    const props = {
      value: 'id',
      label: 'name',
      children: 'children',
    }

    const onQueryChanged = (query: string) => {
      treeRef.value!.filter(query)
    }
    const filterMethod = (query: string, node: any) => {
      return node.name!.includes(query)
    }
    return {
      a,
      query,
      treeRef,
      data,
      props,
      onQueryChanged,
      filterMethod
    };

  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
