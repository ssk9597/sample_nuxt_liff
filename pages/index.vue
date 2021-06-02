<template>
  <div>
    <input type="text" v-model="name" />
    <br />
    <!-- <button @click="addName">送信する</button> -->
  </div>
</template>

<script lang="ts">
import liff from '@line/liff';
import { defineComponent, ref, onMounted } from '@nuxtjs/composition-api';

export default defineComponent({
  setup() {
    const name = ref<string>('');

    // onMounted(() => {
    //   liff.init({
    //     liffId: '1656056842-2mQbxB5R',
    //   });
    //   console.log('test');
    // });

    // const addName = (): void => {
    //   liff
    //     .sendMessages([
    //       {
    //         type: 'text',
    //         text: name.value,
    //       },
    //       {
    //         type: 'text',
    //         text: '送信が完了しました',
    //       },
    //     ])
    //     .then(() => {
    //       liff.closeWindow();
    //     })
    //     .catch(() => {
    //       window.alert('Error sending message');
    //     });

    //   name.value = '';
    // };

    return {
      name,
      // addName,
    };
  },
});
</script>
