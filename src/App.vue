<script setup lang="ts">
import { exampleSetup } from "prosemirror-example-setup";
import { DOMParser, Schema } from "prosemirror-model";
import { schema } from "prosemirror-schema-basic";
import { addListNodes } from "prosemirror-schema-list";
import { EditorState } from "prosemirror-state";
import { EditorView } from "prosemirror-view";

import { onMounted, ref } from "vue";

let editorRef = ref<HTMLElement>();

onMounted(() => {

let modelSchema = new Schema({
    nodes: addListNodes(schema.spec.nodes as any,"paragraph block*", "block"),
    marks:schema.spec.marks,
})

  let state = EditorState.create({ 
    schema,
    doc:DOMParser.fromSchema(modelSchema).parse(editorRef.value as HTMLElement),
    plugins:exampleSetup({schema:modelSchema})
});
  let view = new EditorView(editorRef.value as HTMLElement,{
    state,
  });
});
</script>   

<template>
  <div id="editor" ref="editorRef" contenteditable ></div>
</template>
<style lang="css">
    @import url("./css/reset.css");
    @import url("/node_modules/prosemirror-view/style/prosemirror.css");
    @import url("/node_modules/prosemirror-menu/style/menu.css");
    @import url("/node_modules/prosemirror-gapcursor/style/gapcursor.css");
    @import url("/node_modules/prosemirror-example-setup/style/style.css");
</style>
<style scoped>

#editor {
  width: 50vw;
  height: 50vh;
}
</style>
