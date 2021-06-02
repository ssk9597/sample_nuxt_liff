<template>
  <section class="container">
    <p class="line-id">LINE ID：{{ lineId }}</p>
    <div class="form">
      <div class="control">
        <input class="input" type="text" placeholder="お名前" v-model="formData.name" />
      </div>
      <button class="button is-info is-fullwidth" @click="onSubmit()">送信する</button>
      <button class="button is-light is-fullwidth" @click="handleCancel()">キャンセル</button>
    </div>
  </section>
</template>

<script>
import liff from '@line/liff';

export default {
  data() {
    return {
      formData: {
        name: '',
      },
      lineId: null,
    };
  },
  mounted() {
    liff
      .init({
        liffId: process.env.LIFF_ID,
      })
      .then(() => {
        this.lineId = data.context.userId || null;
      });
  },
  methods: {
    onSubmit() {
      liff
        .sendMessages([
          {
            type: 'text',
            text: `お名前：\n${this.formData.name}`,
          },
          {
            type: 'text',
            text: '送信が完了しました',
          },
        ])
        .then(() => {
          liff.closeWindow();
        });
    },
    handleCancel() {
      liff.closeWindow();
    },
  },
};
</script>

<style>
.container {
  margin: 0 auto;
  padding: 20px;
  min-height: 100vh;
}

.line-id {
  margin-bottom: 30px;
}

.form > * {
  margin-bottom: 10px;
}
</style>
