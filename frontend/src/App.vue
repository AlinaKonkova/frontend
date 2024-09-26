<template>
  <div>
    <h1>Лабораторная работа №1</h1>
    <input v-model="inputValue" placeholder="Введите данные" />
    <button @click="sendData">Отправить</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputValue: ''
    };
  },
  methods: {
    async sendData() {
      try {
        const response = await fetch('http://localhost:8000/api/data/', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({ data: this.inputValue }),
        });
        if (response.ok) {
          console.log('Данные успешно отправлены');
        }
      } catch (error) {
        console.error('Ошибка отправки данных', error);
      }
    },
  },
};
</script>
