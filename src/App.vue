<template>
  <div class="content">
    <h2>Мой список задач</h2>
    <br>
    <input type="text" placeholder="новая задача" v-model="name" @keyup.enter="addList">

    <div class="list_task">
      <ol>
        <li v-for="(item, index) in list" :key="index" @click="selectList(index)" :class="{ 'selected': index === idSelected }">
          {{ item.text }}
        </li>
      </ol>
    </div>
    <button @click="removeList">Удалить</button>
    <button @click="sortList">Сортировать</button>

  </div>
</template>

<script>
export default {
  data() {
    return {
      name: '',
      list: [],
      idSelected: null,
    };
  },
  methods: {
    addList() {
      if (this.name.trim() !== '') {
        this.list.push({ text: this.name, selected: false });
        console.log(this.list);
        this.name = '';
      } else {
        alert('Введите задачу');
      }
    },
    removeList() {
      if (this.idSelected !== null) {
        this.list.splice(this.idSelected, 1);
        console.log(this.list);
        this.idSelected = null; // обнуляем idSelected после удаления
      }
    },
    selectList(index) {
      // Обработка клика по элементу списка для выделения
      this.idSelected = index;
      
    },
    sortList() {
      this.list.sort((a, b) => a.text.localeCompare(b.text));
      console.log(this.list);
    },
  },
};
</script>

<style scoped>
.selected {
  background-color: #cfd8dc;
  cursor: pointer;
}

.content{
  width: 700px;
  height: 80vh;
  background-color:#cefefb;
  border-radius: 20px;
  text-align: center;
  margin-top: 30px;
  border: 4px solid rgb(150, 44, 44);
  justify-content: left;
 
}
.content h2{
  text-transform: uppercase;
  padding-top: 50px;
  padding-bottom: 10px;
  font-size: 40px;
  font-weight: bold;
  letter-spacing: 0.1em;
  
}
.content p{
  padding-bottom: 20px;
}
.content input{
  width: 80%;
  height: 30px;
  font-size: 24px;
  font-family: pattaya;
  letter-spacing: 0.1em;
  margin-left: 10px;
  margin-top: 10px;
  padding: 2px;
  background-color:#dafcfa;
  border: 4px solid rgb(150, 44, 44);
  border-radius: 5px;

}
.content button{
  width: auto;
  height: 50px;
  font-size: 16px;
  font-weight: bold;
  font-family: pattaya;
  letter-spacing: 0.1em;
  margin-top: 30px;
  text-transform: uppercase;
  background-color:#cefefb;
  border: 4px solid rgb(150, 44, 44);
  border-radius: 5px;
  padding-left: 10px;
  padding-right: 10px;
  margin-left: 30px;
}
.content ol{
  width: 80%;
  background-color:#dafcfa;
  font-size: 24px;
  margin-left: 30px;
  
  
}
.content ol li{
  width: 100%;
  margin-left: 10px;
  text-align: left;
  border-bottom: 1px solid rgb(150, 44, 44);
  
}
.list_task{
  width: 60%;
  height:50vh ;
  border: 4px solid rgb(150, 44, 44);
  border-radius: 10px;
  margin-left: 10%;
  margin-top: 5%;
}
</style>

