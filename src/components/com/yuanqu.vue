<template>
  <div>
    <div class=" inline-block">
      <el-button class="inline-block" @click="addshaixuan">+ 添加筛选</el-button>
      <el-tooltip :disabled="display" class="item  inline-block" effect="dark" content="点击搜索框可以直接点选分类，或者直接在其中搜索分类" placement="bottom-start">
        <!-- <el-cascader placeholder="试试搜索：指南" expand-trigger="hover" :options="quYu" filterable change-on-select></el-cascader> -->
        <el-select v-model="value1" placeholder="试试搜索：开发区" clearable filterable>
          <el-option v-for="item in quYu" :key="item.value" :label="item.label" :value="item.value">
            <span style="float: left">{{ item.label }}</span>
            <span style="float: right; color: #8492a6; font-size: 13px">{{ item.num }}</span>
          </el-option>
        </el-select>
      </el-tooltip>
      <el-button class=" inline-block" type="primary" icon="el-icon-search" style="margin-left:10px" @click="sousuo" :loading="$store.state.help.loading.chanye">搜索</el-button>
    </div>
  </div>
</template>

<script>
  import {
    xiugaitijiao
  } from '../../util'
  export default {
    props: {
      display: false
    },
    created() {
      this.$store.dispatch('yuanQu_Ac')
    },
    data() {
      return {
        value1: ''
      }
    },
    computed: {
      quYu() {
        return this.$store.state.yuanQu
      },
    },
    methods: {
      addshaixuan() {
        if (this.$store.state.duoxuan[1].searchValue.length == 0) {
          this.$message.error('请选择第一个筛选条件');
          return;
        } else if (this.$store.state.duoxuan[1].eq == this.$store.state.duoxuan[1].searchValue.length) {
          this.$message.error('请选择一个当前的筛选条件');
          return;
        } else if (this.$store.state.duoxuan[1].searchValue[this.$store.state.duoxuan[1].eq].length == 0) {
          this.$message.error('点击添加条件后请选择新的筛选条件');
          return;
        } else {
          this.$message.success('点击添加条件后请选择新的筛选条件');
          var value = ++this.$store.state.duoxuan[1].eq;
          this.value = '';
          this.initValue = [];
          this.initLabel = [];
          this.$store.commit('changeEq_Mu', {
            value,
            eq: 1
          })
        }
      },
      sousuo() {
         this.$store.state.help.loading.chanye = true;
        xiugaitijiao(this.$store);
       // this.$emit('soule')
        this.$store.dispatch('comBasic_Ac')
        if (this.$route.path == '/') {
          this.$router.push({
            path: '/result/companylist'
          })
        }
      }
    }
  }

</script>

<style>


</style>
