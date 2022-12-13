<template>
<button style="
    position: fixed;
    z-index: 1;
    left: 0;
    right: 0;
    top: 0;
    background: green;
" @click="ss = !ss">显示</button>
  <n-data-table
  v-if="ss"
    :columns="columns"
    :data="data"
    :pagination="pagination"
    :bordered="false"
  />
</template>


<script lang="ts">
import { h, defineComponent ,ref} from "vue";
import { NButton, useMessage } from "naive-ui";
import type { DataTableColumns } from "naive-ui";

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
        tooltip: true,
      },
    },
    {
      title: "Title",
      key: "title",
      ellipsis: {
        tooltip: true,
      },
    },
    {
      title: "Length",
      key: "length",
      ellipsis: {
        tooltip: true,
      },
    },
    {
      title: "Action",
      key: "actions",
      render(row: Song) {
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
];

for (let i = 0; i < 30; i++) {
  data.push({
    no: i,
    title: `Title ${i}`,
    length: "4:18",
  });
}

export default defineComponent({
  setup() {
    const message = useMessage();
    return {
      ss,
      data,
      columns: createColumns({
        play(row: Song) {
          message.info(`Play ${row.title}`);
        },
      }),
      pagination: false as const,
    };
  },
});
</script>