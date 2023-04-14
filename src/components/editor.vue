<script setup lang="ts">
import { Highlight } from '@tiptap/extension-highlight';
import { TextAlign } from "@tiptap/extension-text-align";
import StarterKit from "@tiptap/starter-kit";
import { BubbleMenu, EditorContent, useEditor } from '@tiptap/vue-3';

const editor = useEditor({
  content: `<p>  Shanghai is the largest city by population in the People's Republic of China (PRC) and the largest city proper by population in the world. It is one of the four province-level municipalities of the PRC, with a total population of over 23 million as of 2010. It is a global city, with influence in commerce, culture, finance, media, fashion, technology, and transport. It is a major financial center and the busiest container port in the world.</p>`, // 设置初始内容
  extensions: [
    StarterKit.configure({ // 默认扩展设置
      heading: {
        levels: [1, 2, 3, 4, 5, 6]
      },
      // history:false, // 禁言某个默认扩展 ， 协同扩展中有一个自己 history 可能与与这个冲突，加载 协同扩展时注意禁言
    }),
    Highlight,
    TextAlign.configure({
      types: ['heading', 'paragraph'] // 默认值为空数组，[] 所以需要先配置下
    }),
  ],
  autofocus: true, // 初始化后将光标放入编辑器中
  editable: true, // 默认文本可编辑
  injectCSS: false,// 禁言默认 CSS 加载
})

</script>   

<template>
  <section>
    <editor-content :editor="editor"></editor-content>
  </section>
  <bubble-menu v-if="editor" :editor="editor" :tippy-options="{ duration: 200 }">
    <button @click="editor.chain().focus().toggleBold().run()">加粗</button>
    <button @click="editor.chain().focus().toggleItalic().run()">斜体</button>
    <button @click="editor.chain().focus().toggleHighlight().run()">高亮</button>
    <button @click="editor.chain().focus().setTextAlign('left').run()">左对齐</button>
    <button @click="editor.chain().focus().setTextAlign('center').run()">居中对齐</button>
    <button @click="editor.chain().focus().setTextAlign('right').run()">右对齐</button>
    <button @click="editor.chain().focus().setTextAlign('justify').run()">两端对齐</button>
  </bubble-menu>
</template>
 
<style scoped></style>
