<template>
  <div class="w-full h-[55px] grid grid-cols-9 gap-1 py-1">
    <ServerDetails />
    <SetupDetails class="col-start-4 col-end-7 p-2" :list="setupsList" @select-setup="selectSetup" @server-view="serverView" />
    <NetworkDetails />
  </div>
</template>
<script setup>
import { useMultiSetups } from "@/composables/multiSetups";
import { useSetups } from "@/store/setups";
import { computed } from "vue";
import NetworkDetails from "../../../edit-page/components/edit/header/NetworkDetails.vue";
import ServerDetails from "../../../edit-page/components/edit/header/ServerDetails.vue";
import SetupDetails from "../../../edit-page/components/edit/header/SetupDetails.vue";

const setupStore = useSetups();
const { getSelectedSetup, getServerView } = useMultiSetups();

const setupsList = computed(() => {
  return setupStore.allSetups;
});

const selectSetup = (setup) => {
  getSelectedSetup(setup);
};

const serverView = () => {
  getServerView();
};

// End of script
</script>
<style scoped>
.fade-move,
.fade-enter-active,
.fade-leave-active {
  transition: all 0.5s cubic-bezier(0.55, 0, 0.1, 1);
}

/* 2. declare enter from and leave to state */
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: scaleY(0.01) translate(30px, 0);
}

/* 3. ensure leaving items are taken out of layout flow so that moving
      animations can be calculated correctly. */
.fade-leave-active {
  position: absolute;
}
</style>
