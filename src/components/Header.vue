<template>
  <header
    class="w-full h-14 shrink-0 flex flex-row justify-center items-center"
  >
    <div
      class="w-full md:max-w-5xl lg:max-w-7xl h-full flex flex-row justify-center items-center px-0 sm:px-4"
    >
      <div class="h-full flex flex-row justify-start items-center">
        <span
          class="h-full flex flex-row justify-center items-center cursor-pointer font-semibold mr-2 px-3 hover:bg-light"
          @click="handleSetTokenBtnClick"
        >
          {{ token ? "Edit" : "Add" }} Access Token
        </span>
      </div>

      <div class="h-full flex md:hidden flex-row justify-end items-center">
        <span
          class="relative h-full w-10 px-3 flex flex-row justify-center items-center cursor-pointer font-semibold text-light hover:bg-zinc-800"
          @click="handleToggleDropMenuBtnClick"
        >
          <span
            class="w-4 transition-all h-px bg-light absolute top-1/2"
            :class="state.showDropMenu ? 'w-6 rotate-45' : '-mt-1'"
          ></span>
          <span
            class="w-4 transition-all h-px bg-light absolute top-1/2"
            :class="state.showDropMenu ? 'hidden' : ''"
          ></span>
          <span
            class="w-4 transition-all h-px bg-light absolute top-1/2"
            :class="state.showDropMenu ? 'w-6 -rotate-45' : 'mt-1'"
          ></span>
        </span>
      </div>
    </div>
  </header>
  <TokenSettingDialog
    v-if="state.showSetTokenDialog"
    @close="handleSetTokenDialogClose"
  />
</template>

<script lang="ts" setup>
import { computed, reactive } from "vue";
import useAppStore from "../store";
import TopBanner from "./TopBanner.vue";
import GitHubStarButton from "./GitHubStarButton.vue";
import TokenSettingDialog from "./TokenSettingDialog.vue";

interface State {
  showDropMenu: boolean;
  showSetTokenDialog: boolean;
}

const store = useAppStore();
const state = reactive<State>({
  showDropMenu: false,
  showSetTokenDialog: false,
});

const token = computed(() => {
  return store.token;
});

const handleSetTokenBtnClick = () => {
  state.showSetTokenDialog = true;
};

const handleSetTokenDialogClose = () => {
  state.showSetTokenDialog = false;
};

const handleToggleDropMenuBtnClick = () => {
  state.showDropMenu = !state.showDropMenu;
};
</script>
