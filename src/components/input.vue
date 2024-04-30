<script>
export default {
  data () {
    return {

    };
  },
  methods: {
  },
  props: {
    changeAmount: {
      type: Function,
      required: true
    },
    convert: {
      type: Function,
      required: true
    },
  }
}  
</script>

<template>
  <input type="number" @input="changeAmount($event.target.value)" placeholder='Введите значение'><br>
  <button @click="convert()">Конвертировать</button>
</template>

<style scoped>
input { 
  outline: none;
  width: 500px;
  position: relative;
  top: -20px;
  font-size: 1.2em;
  border-radius: 3px;
  border: 0;
  padding: 10px 15px;
  background: #fafafa;
  color: #333;
}

button {
  display: inline-block;
  padding: 10px 20px;
  font-size: 16px;
  font-weight: bold;
  text-align: center;
  text-decoration: none;
  cursor: pointer;
  border: none;
  border-radius: 5px;
  background-color: #0453fd; /* Зеленый цвет фона */
  color: white; /* Белый цвет текста */
  transition: background-color 0.3s ease;
  margin-bottom: 20px;
}

button:hover {
  background-color: #0004ff; /* Темно-зеленый цвет фона */
}
</style>