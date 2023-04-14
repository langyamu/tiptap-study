<script setup lang="ts">
import { Highlight } from '@tiptap/extension-highlight';
import { TextAlign } from "@tiptap/extension-text-align";
import StarterKit from "@tiptap/starter-kit";
import { EditorContent, useEditor } from '@tiptap/vue-3';

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
    })
  ],
  autofocus: true, // 初始化后将光标放入编辑器中
  editable: true, // 默认文本可编辑
  injectCSS: false,// 禁言默认 CSS 加载
})

</script>   

<template>
        <section >
        <header class="fixed-menu">
          <!--
          --  editor :: tiptap 编辑器实例
          -- chain() :: 告诉编辑器要执行多个命令（commands）
                  -- focus() :: 聚焦到编辑器
                                用户在点击菜单按钮时，编辑器会失去焦点，可以通过这个命令focus回编辑器，这样不打断用户的写作流程
                  -- toggleBold() ::  选定内容添加粗体 mark 或 移除粗体 mark
                  -- run() :: 执行命令链
                -->
            <!--
                -- :class="{ 'is-active': editor?.isActive('bold') }"
                -- 当用户点击按钮时 会切换 ‘‘is-active“ 这个 class 的显示状态，不一定与加粗mark与移除加粗mark的行为一致
              -->
              <button :class="{ 'is-active': editor?.isActive('bold') }" @click="editor?.chain().focus().toggleBold().run()">加粗</button>

            <!--
                -- :class="{ 'is-active': editor?.isActive('highlight') }"
                -- 当用户点击按钮时 会切换 ‘‘is-active“ 这个 class 的显示状态，不一定与高亮mark与移除高亮mark的行为一致
              -->
              <button :class="{ 'is-active': editor?.isActive('highlight') }" @click="editor?.chain().focus().toggleHighlight().run()">高亮</button>

              <button :class="{ 'is-active': editor?.isActive({ textAlign: 'left' }) }" @click="editor?.chain().focus().setTextAlign('left').run()">左对齐</button>
              <button :class="{ 'is-active': editor?.isActive({ textAlign: 'center' }) }" @click="editor?.chain().focus().setTextAlign('center').run()">居中对齐</button>
              <button :class="{ 'is-active': editor?.isActive({ textAlign: 'right' }) }" @click="editor?.chain().focus().setTextAlign('right').run()">右对齐</button>
              <!-- 
                -- https://zhuanlan.zhihu.com/p/129268155
                -- 两端对齐，文本太少没有效果
               -->
              <button :class="{ 'is-active': editor?.isActive({ textAlign: 'justify' }) }" @click="editor?.chain().focus().setTextAlign('justify').run()">两端对齐</button>

            </header>
            <editor-content :editor="editor"></editor-content>
          </section>
</template>
 
<style scoped>
.fixed-menu{
 display: flex;
}
.fixed-menu button{
  width: 5rem;
  align-items: center;
  margin-right: 1rem;
}
</style>
