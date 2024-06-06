<script setup lang="ts">
import { onMounted, ref, watch, computed } from 'vue';
import IconCard from './IconCard.vue';
import type { IIconCardProps } from './IconCard.vue';
import { loadIcons } from './../helpers/load-icons';

const iconStyles = ref<string[]>(['bold', 'broken', 'bulk', 'linear', 'outline', 'twotone']);
const selectedIconType = ref<string>('bold');
const queryIcon = ref<string>('');

const icons = ref<IIconCardProps[]>([]);

const pending = ref<boolean>(true);

onMounted(async () => {
  icons.value = await loadIcons('bold');
  pending.value = false;
});

watch(selectedIconType, async (type) => {
  pending.value = true;
  icons.value = await loadIcons(type);
  pending.value = false;
});

// TODO: up speed icons
const filteredIcons = computed(() => {
  if (!queryIcon.value) {
    return icons.value;
  }

  return icons.value.filter((icon) => 
    icon.componentName.toLowerCase().includes(queryIcon.value.toLowerCase())
  );
});
</script>

<template>
  <div style="max-width: 1140px; margin: 0 auto; padding: 0 1rem;">
    <a-flex vertical align="center">
      <a-segmented v-model:value="selectedIconType" :options="iconStyles" />

      <a-input
        v-model:value="queryIcon"
        size="large"
        placeholder="Search icons..."
        style="max-width: 500px; margin-top: 1rem;"
      />
    </a-flex>

    <a-flex>
      <div v-if="pending" style="width: 100%; margin-top: 3rem;">
        <a-flex justify="center">
          <a-spin size="large" />
        </a-flex>
      </div>
      
      <div v-else>
        <a-row :gutter="[16, 16]" style="margin-top: 2rem;">
          <a-col
            v-for="icon in filteredIcons"
            :key="icon.componentName"
            class="gutter-row"
            :span="6"
          >
            <IconCard v-bind="icon" />
          </a-col>
        </a-row>
      </div>
    </a-flex>
  </div>
</template>
