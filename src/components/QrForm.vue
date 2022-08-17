<script setup lang="ts">
import { reactive, ref } from "@vue/reactivity";
import type { Ref } from "vue";

const options = reactive([
  {
    size: "100",
    selected: true,
  },
  {
    size: "200",
    selected: false,
  },
  {
    size: "300",
    selected: false,
  },
  {
    size: "400",
    selected: false,
  },
  {
    size: "500",
    selected: false,
  },
  {
    size: "600",
    selected: false,
  },
  {
    size: "700",
    selected: false,
  },
]);

const url = ref("");
const qrCodeSize: Ref<string> = ref("100");

const emit = defineEmits({
  // Validate submit event
  qr: ({ url, qrCodeSize }) => {
    if (url && qrCodeSize) {
      return true;
    } else {
      alert("Invalid submit event payload!");
      return false;
    }
  },
});

const submit = () => {
  emit("qr", { url, qrCodeSize });
};
</script>

<template>
  <form @submit.prevent="submit" ref="generateForm" class="mt-4">
    <input
      v-model="url"
      type="url"
      placeholder="Enter a URL"
      class="w-full border-2 border-gray-200 rounded p-3 text-grey-dark mr-2 focus:outline-none mb-5"
    />
    <select
      v-model="qrCodeSize"
      class="w-full border-2 border-gray-200 rounded p-3 text-grey-dark mr-2 focus:outline-none"
      name="size"
      id="size"
    >
      <option
        :value="size"
        v-for="({ size, selected }, index) in options"
        :key="index"
        :selected="selected"
      >
        {{ size }}
      </option>
    </select>
    <button
      class="bg-gray-600 rounded w-full text-white py-3 px-4 mt-5 hover:bg-black"
      type="submit"
    >
      Generate QR Code
    </button>
  </form>
</template>
