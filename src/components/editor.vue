<script setup lang="ts">
import StarterKit from "@tiptap/starter-kit";
import { EditorContent, useEditor } from '@tiptap/vue-3';
//  获取 prosemirror 内部API
// import { EditorState } from "@tiptap/pm/state";
// EditorState.create()
// tiptap 内部封装好了， 支持以下包的获取，省的一个一个下包了
// @tiptap/pm/changeset
// @tiptap/pm/collab
// @tiptap/pm/commands
// @tiptap/pm/dropcursor
// @tiptap/pm/gapcursor
// @tiptap/pm/history
// @tiptap/pm/inputrules
// @tiptap/pm/keymap
// @tiptap/pm/markdown
// @tiptap/pm/menu
// @tiptap/pm/model
// @tiptap/pm/schema-basic
// @tiptap/pm/schema-list
// @tiptap/pm/state
// @tiptap/pm/tables
// @tiptap/pm/trailing-node
// @tiptap/pm/transform
// @tiptap/pm/view

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
