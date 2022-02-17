<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import artical_list from './assets/artical_list.json';
import artical_contents from './assets/artical_contents.json';

import ArticalViewVue from './components/ArticalView.vue';
import { reactive } from 'vue';

const dict = reactive({
  tempData: {
    showDialog: false,
    article_we_choose: {
      title: '',
      content: [] as string[],
      audio_url: '',
    }
  },
});
</script>

<template>
  <template class="mb-10" v-for="item in artical_list" :key="item.article_link">
    <div class="flex justify-center m-20">
      <div class="flex justify-between h-24">
        <div class="bg-indigo-200 w-96">
          <div>{{ item.title }}</div>
          <div
            class="text-red-600 mt-10 text-base"
            @click="() => {
              if (item.article_link in artical_contents) {
                dict.tempData.article_we_choose = {
                  title: item.title,
                  // @ts-ignore: Unreachable code error
                  content: artical_contents[item.article_link].content,
                  // @ts-ignore: Unreachable code error
                  audio_url: artical_contents[item.article_link].audio_url,
                };
                dict.tempData.showDialog = true;
              }
              dict.tempData.showDialog = true;
            }"
          >Check</div>
        </div>
        <div class="bg-blue-300 w-48">
          <div>{{ item.author }}</div>
        </div>
      </div>
    </div>
  </template>

  <el-dialog
    v-model="dict.tempData.showDialog"
    :title="dict.tempData.article_we_choose.title"
    width="90%"
  >
    <ArticalViewVue
      :content="dict.tempData.article_we_choose.content"
      :audio_url="dict.tempData.article_we_choose.audio_url"
    ></ArticalViewVue>
    <template #footer></template>
  </el-dialog>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
