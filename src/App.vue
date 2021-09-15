<script setup>
import { onMounted, ref } from "vue";

const node1 = ref(null);
const node2 = ref(null);
const node3 = ref(null);

const class1 = ref("");
const class2 = ref("");
const class3 = ref("");

const className1 = `
p-4
mt-4
bg-gray-200
transition-all
whitespace-pre-wrap
flex flex-col
dark:(bg-gray-800
text-gray-300)
`;

const className2 = `
    p-4
    mt-4
    bg-gray-200
    transition-all
    whitespace-pre-wrap
    flex flex-col
    dark:(bg-gray-800
    text-gray-300)
`;

function getClass(node) {
  return node.getAttribute("class").replace(/\s+/g, " ").split(" ").join("\n");
}

onMounted(() => {
  class1.value = getClass(node1.value);
  class2.value = getClass(node2.value);
  class3.value = getClass(node3.value);
});
</script>

<template>
  <div>
    <h1>Vite + Vue3 + WindiCSS</h1>
    <h2>Demonstration of multiline variant group bug</h2>
    <br />
    <p>
      When defining a variant group over multiple lines, WindiCSS will generate
      strings like <code>${variant}:</code> if those new lines have leading
      spaces.
    </p>

    <div ref="node1" :class="className1">
      <strong>Output (class defined in script) (no leading spaces)</strong
      >{{ class1 }}
    </div>

    <div ref="node2" :class="className2">
      <strong>Output (class defined in script) (4 leading spaces)</strong
      >{{ class2 }}
    </div>

    <div
      ref="node3"
      class="
        p-4
        mt-4
        bg-gray-200
        transition-all
        whitespace-pre-wrap
        flex flex-col
        dark:(bg-gray-800
        text-gray-300)
      "
    >
      <strong
        >Output (class defined in template) (will always have leading
        spaces)</strong
      >{{ class3 }}
    </div>
  </div>
</template>
