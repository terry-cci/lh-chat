<script lang="ts">
export type StringHighlightInfo = {
  content: string;
  highlighted: boolean;
};
</script>

<script setup lang="ts">
import { computed } from "vue";
const props =
  defineProps<{ text: string; highlight: string; highlightClass?: string[] }>();

const highlightInfo = computed(() => {
  if (props.highlight) {
    const result: StringHighlightInfo[] = [];
    const matches = props.text.matchAll(
      new RegExp(props.highlight.trim(), "g")
    );

    let startIdx = 0;
    for (const m of matches) {
      if (m.index !== undefined && startIdx < m.index)
        result.push({
          content: props.text.substring(startIdx, m.index),
          highlighted: false,
        });
      result.push({
        content: m[0],
        highlighted: true,
      });
      if (m.index !== undefined) startIdx = m.index + m[0].length;
    }
    result.push({
      content: props.text.substring(startIdx),
      highlighted: false,
    });
    return result;
  } else return [{ content: props.text, highlighted: false }];
});
</script>

<template>
  <span
    v-for="info in highlightInfo"
    :class="info.highlighted && highlightClass"
  >
    {{ info.content }}
  </span>
</template>
