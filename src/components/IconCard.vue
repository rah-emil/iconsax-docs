<script setup lang="ts">
export interface IIconCardProps {
  componentName: string;
  svg: string;
}
const props = defineProps<IIconCardProps>();
</script>

<template>
  <div class="icon-card">
    <span v-html="props.svg" style="width: 50px; display: inline-block; margin-right: 0.5rem;"></span>

    <a-typography-text code>
      {{ props.componentName }}
    </a-typography-text>
  </div>
</template>

<style>
.icon-card {
  background-color: #fff;
  padding: 1rem;
  border-radius: 1rem;
  box-shadow: 5px 5px 8px rgba(0,0,0,.1);
  display: flex;
  flex-flow: row nowrap;
  color: #2B1E0F;
}
</style>
