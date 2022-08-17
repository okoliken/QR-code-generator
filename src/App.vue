<script setup lang="ts">
import Header from "../src/components/header.vue";
import Spinner from "./components/spinner.vue";
import QrForm from "../src/components/QrForm.vue";
import { ref } from "@vue/reactivity";
import type { Ref } from "vue";

const spinner: Ref<boolean> = ref(false);
const qrCode = ref(null);
const qr = document.getElementById("qrCode");

const convertQrCode = ({ url, qrCodeSize }) => {
      clearUI();
  // console.log(url, qrCodeSize, qrCode.value.src);
  if (url.value === "") {
    alert("Please enter a URL");
  } else {


    showSpinner();

    // Show spinner for 1 sec
    setTimeout(() => {
      hideSpinner();
      generateQRCode(url.value, qrCodeSize.value);

      // Generate the save button after the qr code image src is ready
      setTimeout(() => {
        // Get save url.
        const qr = document.getElementById("qrCode");
        const saveUrl = qr.querySelector("img").src;
        // Create save button

        console.log(saveUrl);
        createSaveBtn(saveUrl);
      }, 50);
    }, 1000);
  }
};

const generateQRCode = (url: string, size: string) => {
  const qrcode = new QRCode("qrCode", {
    text: url,
    width: size,
    height: size,
  });
  return qrcode;
};

const showSpinner = () => {
  spinner.value = true;
};
const hideSpinner = () => {
  spinner.value = false;
};
const createSaveBtn = (saveUrl) => {
  const link = document.createElement("a");
  link.id = "save-link";
  link.classList =
    "bg-red-500 hover:bg-red-700 text-white font-bold py-2 rounded w-1/3 m-auto my-5";
  link.href = saveUrl;
  link.download = "qrcode";
  link.innerHTML = "Save Image";
  document.getElementById("generated").appendChild(link);
};

const clearUI = () => {
  const qr = document.getElementById("qrCode");
  qr.innerHTML = "";
  const saveBtn = document.getElementById("save-link");
  if (saveBtn) {
    saveBtn.remove();
  }
};
</script>

<template>
  <div>
    <Header />
    <main>
      <div
        class="flex flex-col-reverse align-center justify-center m-auto md:max-w-4xl p-10 md:flex-row"
      >
        <div class="w-full md:w-2/3 mr-24">
          <h1 class="text-3xl font-bold mb-5 md:text-4xl">QR Code Generator</h1>
          <p class="mb-4">
            QR Codes allow smartphone users to access your website simply and
            quickly.
          </p>
          <p>
            Enter your URL below to generate a QR Code and download the image.
          </p>

          <qr-form @qr="convertQrCode" />
        </div>
        <div class="w-full md:w-1/3 self-center">
          <img
            class="w-1/2 m-auto mb-10 md:w-full"
            src="../src/assets/img/qr-code.svg"
            alt=""
          />
        </div>
      </div>

      <div
        id="generated"
        role="status"
        class="max-w-5xl m-auto flex flex-col text-center align-center justify-center mt-20"
      >
        <!-- Spinner -->

        <spinner v-if="spinner" />

        <!-- End -->
        <div id="qrCode" class="m-auto"></div>
      </div>
    </main>
  </div>
</template>

<style scoped></style>
