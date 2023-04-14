<script setup lang="ts">
import StarterKit from "@tiptap/starter-kit";
import { EditorContent, useEditor } from '@tiptap/vue-3';

const editor = useEditor({
  content:'<p>hello world</p>',
  extensions:[
    StarterKit
  ]
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
