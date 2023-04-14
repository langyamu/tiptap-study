<script setup lang="ts">
import StarterKit from "@tiptap/starter-kit";
import { EditorContent, useEditor } from '@tiptap/vue-3';

const editor = useEditor({
  content:'<p>hello world</p>', // 设置初始内容
  extensions:[
    StarterKit.configure({ // 默认扩展设置
      heading:{
        levels:[1,2,3,4,5,6]
      },
      // history:false, // 禁言某个默认扩展 ， 协同扩展中有一个自己 history 可能与与这个冲突，加载 协同扩展时注意禁言
    })
  ],
  autofocus: true, // 初始化后将光标放入编辑器中
  editable:true, // 默认文本可编辑
  injectCSS: false,// 禁言默认 CSS 加载
})
</script>   

<template>
  <editor-content :editor="editor"></editor-content>
</template>
<style lang="css">
</style>
<style scoped>

#editor {
  width: 50vw;
  height: 50vh;
}
</style>
