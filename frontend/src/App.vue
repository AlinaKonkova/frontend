<template>
  <div>
    <h1>Лабораторная работа №1.ver2</h1>
    <input v-model="inputValue" placeholder="Введите данные" />
    <button @click="sendData">Отправить</button>
    <button @click="fetchData">Получить данные</button>
    <div v-if="fileData">Содержимое файла: {{ fileData }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputValue: '',
      fileData: ''
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
    async fetchData() {
      try {
        const response = await fetch('http://localhost:8000/api/data/get');
        const result = await response.json();
        this.fileData = result.data;
        console.log('Данные успешно получены');
      } catch (error) {
        console.error('Ошибка получения данных', error);
      }
    },
  },
};
</script>
