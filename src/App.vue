<script setup lang="ts">
import Header from "../src/components/header.vue";
import Spinner from "./components/spinner.vue";
import QrForm from '../src/components/QrForm.vue'
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

          <qr-form />
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
        class="max-w-5xl m-auto flex flex-col text-center align-center justify-center mt-20"
      >
        <!-- Spinner -->

        <spinner />

        <!-- End -->
        <div id="qrcode" class="m-auto"></div>
      </div>
    </main>
  </div>
</template>

<style scoped></style>
