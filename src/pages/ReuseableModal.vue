<template>
  <section class="flex flex-wrap w-full">
    <div class="m-auto">
      <h1 class="text-2xl my-5">Re-useable Modal</h1>
      <Modal v-if="isRedModalOpen" @close="isRedModalOpen = false">
        <h1 class="text-red-500">Red Modal</h1>
      </Modal>
      <button class="border rounded px-2 mx-4" @click="isRedModalOpen = true">
        Red Modal
      </button>
      <Modal v-if="isBlueModalOpen" @close="isBlueModalOpen = false">
        <h1 class="text-blue-500">Blue Modal</h1>
      </Modal>
      <button class="border rounded px-2 mx-4" @click="isBlueModalOpen = true">
        Blue Modal
      </button>
    </div>
  </section>
</template>

<script>
import Modal from "../components/Modal";
import { ref } from "vue";

export default {
  components: { Modal },
  setup() {
    const isRedModalOpen = ref(false);
    const isBlueModalOpen = ref(false);
    return { isRedModalOpen, isBlueModalOpen };
  },
};
</script>

<style></style>
