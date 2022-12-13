<script setup lang="ts">
import { h, defineComponent ,ref} from "vue";
import { NButton, useMessage } from "naive-ui";
import type { DataTableColumns } from "naive-ui";


defineProps<{ msg: string }>()

const count = ref(0)



const ss = ref(true)
type Song = {
  no: number;
  title: string;
  length: string;
};

const createColumns = ({
  play,
}: {
  play: (row: Song) => void;
}): DataTableColumns<Song> => {
  return [
    {
      title: "No",
      key: "no",
      ellipsis: {
        // tooltip: true,
      },
    },
    {
      title: "Title",
      key: "title",
      ellipsis: {
        // tooltip: true,
      },
    },
    {
      title: "Length",
      key: "length",
      ellipsis: {
        // tooltip: true,
      },
    },
    {
      title: "Action",
      key: "actions",
      render(row) {
        return h(
          NButton,
          {
            strong: true,
            tertiary: true,
            size: "small",
            onClick: () => play(row),
          },
          { default: () => "Play" }
        );
      },
    },
  ];
};

const data: Song[] = [
  { no: 3, title: "Wonderwall", length: "4:18" },
  { no: 4, title: "Don't Look Back in Anger", length: "4:48" },
  { no: 12, title: "Champagne Supernova", length: "7:27" },
];

for (let i = 0; i < 100; i++) {
  data.push({
    no: i,
    title: `Title ${i}`,
    length: "4:18",
  });
}

    const message = useMessage();
const columns = createColumns({
        play(row: Song) {
          message.info(`Play ${row.title}`);
        },
      })
</script>

<template>
  <h1>{{ msg }}</h1>
<button style="
    position: fixed;
    z-index: 1;
    left: 0;
    right: 0;
    top: 0;
    background: green;
" @click="ss = !ss">dd</button>
  <n-data-table
  v-if="ss"
    :columns="columns"
    :data="data"
    :bordered="false"
  />
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
