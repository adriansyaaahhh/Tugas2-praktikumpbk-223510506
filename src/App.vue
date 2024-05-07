<template>
  <div class="container">
    <div class="content" :class="{ 'custom-class': isCustomClass }">
      <div class="input-container">
        <label for="name">Masukkan nama Anda:</label>
        <input type="text" v-model="name" @input="changeColor" placeholder="Nama Anda">
        <label for="name">Ukuran font:</label>
        <input type="number" v-model="fontSize" min="10" max="30" placeholder="Ukuran Font">
        <button @click="addNameToList" class="ok-button">OK</button>
      </div>
      <p class="result" :style="{ color: nameColor, fontSize: fontSize + 'px' }">Halo, {{ name }}</p>
      <div class="list-container" style="max-height: 100px; overflow-y: auto;">
        <ul>
          <li v-for="(item, index) in nameList" :key="index" :style="{ color: item.color, fontSize: item.fontSize + 'px' }">{{ item.name }}</li>
        </ul>
      </div>
    </div>
  </div>
</template>



<script>
export default {
  data() {
    return {
      name: '',
      nameColor: 'black',
      fontSize: 20,
      nameList: []
    };
  },
  methods: {
    changeColor() {
      this.nameColor = this.getRandomColor();
    },
    getRandomColor() {
      return '#' + Math.floor(Math.random() * 16777215).toString(16);
    },
    addNameToList() {
      if (this.name.trim() !== '') {
        this.nameList.unshift({ name: this.name, color: this.nameColor, fontSize: this.fontSize });
        this.name = '';
        this.nameColor = 'black';
        this.fontSize = 20;
      }
    }
  }
};
</script>

<style>
.container {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}


.content {
  background: #494747;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  padding: 20px;
  max-width: 400px;
  width: 100%;
}


.input-container {
  background-color: #ccc;
  border-radius: 5px;
  padding: 10px;
  margin-bottom: 20px;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
}

.input-container label {
  display: block;
  margin-bottom: 5px;
  color: #333;
  font-weight: bold;
}

.input-container input {
  width: calc(70% - 10px);
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
  font-size: 18px;
}

.input-container input[type="number"] {
  width: 30%; 
  padding: 12px; 
  font-size: 18px;
  border: 2px solid #ccc; 
  border-radius: 5px; 
}

.input-container .ok-button {
  width: calc(25% - 10px);
  padding: 13px;
  margin-left: 5px;
  margin-top: 10px;
  border: none;
  border-radius: 5px;
  background-color: #fafafa;
  transition:background-color 0.3s;
  color: #333;
  cursor: pointer;
  font-size: 16px;
  font-weight: bold;
}
.input-container .ok-button:hover {
  background-color: #999;
}

.result {
  margin-bottom: 20px;
  font-size: 24px;
  font-weight: bold;
  color: #333;
}

.list-container ul {
  padding: 0;
  list-style-type: none;
}

.list-container li {
  margin-bottom: 5px;
  padding: 10px;
  border-bottom: 1px solid #ccc;
}

.list-container li:last-child {
  border-bottom: none;
}
</style>
