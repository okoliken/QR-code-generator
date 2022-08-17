<script setup>
import { reactive, ref } from "@vue/reactivity";

const options = reactive([
  {
    size: "100x100",
    selected: true,
  },
  {
    size: "200x200",
    selected: false,
  },
  {
    size: "300x300",
    selected: false,
  },
  {
    size: "400x400",
    selected: false,
  },
  {
    size: "500x500",
    selected: false,
  },
  {
    size: "600x600",
    selected: false,
  },
  {
    size: "700x700",
    selected: false,
  },
]);

const url = ref('')
</script>

<template>
  <form ref="generateForm" class="mt-4">
    <input
      v-model="url"
      type="url"
      placeholder="Enter a URL"
      class="w-full border-2 border-gray-200 rounded p-3 text-grey-dark mr-2 focus:outline-none mb-5"
    />
    <select
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

<style></style>
