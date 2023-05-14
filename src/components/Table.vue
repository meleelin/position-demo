<template lang="pug">
table.border-collapse.border.border-slate-300.table-auto.w-full
  thead
    tr
      th.border.border-slate-300.px-3.py-2 Event
      template(v-for="(item, index) in titles", :key="index")
        th.border.border-slate-300.px-3.py-2 {{ item }}
  tbody
    tr
      td.border.border-slate-300.text-center.px-3.py-2 X
      td.border.border-slate-300.text-center.px-3.py-2 {{ contents.client.x }}
      td.border.border-slate-300.text-center.px-3.py-2 {{ contents.offset.x }}
      td.border.border-slate-300.text-center.px-3.py-2 {{ contents.layer.x }}
      td.border.border-slate-300.text-center.px-3.py-2 {{ contents.screen.x }}
      td.border.border-slate-300.text-center.px-3.py-2 {{ contents.page.x }}
    tr
      td.border.border-slate-300.text-center.px-3.py-2 Y
      td.border.border-slate-300.text-center.px-3.py-2 {{ contents.client.y }}
      td.border.border-slate-300.text-center.px-3.py-2 {{ contents.offset.y }}
      td.border.border-slate-300.text-center.px-3.py-2 {{ contents.layer.y }}
      td.border.border-slate-300.text-center.px-3.py-2 {{ contents.screen.y }}
      td.border.border-slate-300.text-center.px-3.py-2 {{ contents.page.y }}
</template>
<script>
import { reactive, ref, watch, watchEffect } from "vue";
export default {
  setup() {
    const titles = ref(["client", "offset", "layer", "screen", "page"]);
    const contents = reactive({
      client: { x: 0, y: 0 },
      offset: { x: 0, y: 0 },
      layer: { x: 0, y: 0 },
      screen: { x: 0, y: 0 },
      page: { x: 0, y: 0 },
    });

    // watch(
    //   () => contents,
    //   (nV, oV) => {
    //     console.log("it's changed");
    //   },

    //   { deep: true }
    // );
    window.addEventListener("mousemove", (e) => {
      // console.log({ e });

      const {
        clientX,
        clientY,
        screenX,
        screenY,
        offsetX,
        offsetY,
        layerX,
        layerY,
        pageX,
        pageY,
      } = e;
      // client
      contents.client.x = clientX;
      contents.client.y = clientY;

      // screen
      contents.screen.x = screenX;
      contents.screen.y = screenY;

      // offset
      contents.offset.x = offsetX;
      contents.offset.y = offsetY;

      // layer
      contents.layer.x = layerX;
      contents.layer.y = layerY;

      // page
      contents.page.x = pageX;
      contents.page.y = pageY;
    });
    return { titles, contents };
  },
};
</script>

<style>
</style>