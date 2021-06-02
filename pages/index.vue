<template>
  <div>
    <input type="text" v-model="name" />
    <br />
    <button @click="addName">送信する</button>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted } from '@nuxtjs/composition-api';
import liff from '@line/liff';

declare global {
  interface Window {
    liff: any;
  }
}
window.liff = window.liff || {};

export default defineComponent({
  setup() {
    const name = ref<string>('');

    onMounted(async () => {
      await window.liff.init({
        liffId: process.env.LIFF_ID,
      });
    });

    const addName = (): void => {
      const idToken = liff.getDecodedIDToken();
      alert(idToken);
      window.liff
        .sendMessages([
          {
            type: 'text',
            text: name.value,
          },
        ])
        .then(() => {
          window.liff.closeWindow();
        })
        .catch(() => {
          window.alert('Error sending message');
          window.liff.closeWindow();
        });

      name.value = '';
    };

    return {
      name,
      addName,
    };
  },
});
</script>
