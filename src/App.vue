<script setup lang="ts">
import AppHeader from './components/AppHeader.vue';
import AppIcons from './components/AppIcons.vue';
</script>

<template>
  <a-space direction="vertical" style="width: 100%;">
    <a-layout style="min-height: 100vh;">
      <AppHeader />

      <a-layout-content>
        <AppIcons />
      </a-layout-content>
    </a-layout>
  </a-space>
</template>
