<script setup>
import { ref } from "vue";
import { filterData } from "../service/service";

const data = ref(null);
const inputValue = ref(null);

async function getFilterData() {
  if (inputValue.value.length == 0) {
    data.value = null;
  } else {
    const result = await filterData(inputValue);
    data.value = result;
  }
}

function getClickedItem(item) {
  inputValue.value = item;
  data.value = "";
}
</script>

<template>
  <div class="container">
    <input class="input" v-model="inputValue" @input="getFilterData()" />

    <div class="list" v-if="data">
      <div class="filter" v-if="data.length > 0">
        <ul>
          <li v-for="item in data" @click="getClickedItem(item)">
            {{ item }}
          </li>
        </ul>
      </div>
      <div class="filter" v-else>
        <ul class="filter_else">
          <li>Herhangi bir değer bulunamadı.</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 100px 250px 0px 250px;
  flex-direction: column;

  
  .input {
    width: 60%;
    margin: 50px 50px 0px 50px;
    height: 50px;
    border-radius: 25px;
    font-size: 55px;
    text-align: 5px;
    padding: 15px;
  }
  .list{
    height: auto;
    margin: -30px;
  }
  .filter {
    background-color: orange;
    height: auto;
    width: 100%;
    font-size: 35px;
    border-radius: 20px;

    ul {
      width: 800px;
      list-style-type: none;
      padding: 30px;
    }
    li {
      background-color: rgb(245, 205, 131);
      border-radius: 10px;
      margin-top: 5px;
      padding: 5px;
    }
    li:hover{
      background-color: rgb(244, 196, 108);
      border-radius: 10px;
      margin-top: 5px;
    }
  }
  .filter_else {
      background-color: red;
      border-radius: 25px;
      font-size: 35px;
      text-align: 5px;
      li {
        background-color: rgb(255, 0, 0);
        border-radius: 10px;
        margin-top: 5px;
      }
  }
}
</style>
