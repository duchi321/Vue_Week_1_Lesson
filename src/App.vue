<script setup>
import { ref } from 'vue'
const menu = ref([
  {
    id: 1,
    product: '珍珠奶茶',
    description: '香濃奶茶搭配QQ珍珠',
    price: 50,
    stock: 20
  },
  {
    id: 2,
    product: '冬瓜檸檬',
    description: '清新冬瓜配上新鮮檸檬',
    price: 45,
    stock: 18
  },
  {
    id: 3,
    product: '翡翠檸檬',
    description: '綠茶與檸檬的完美結合',
    price: 55,
    stock: 34
  },
  {
    id: 4,
    product: '四季春茶',
    description: '香醇四季春茶，回甘無比',
    price: 45,
    stock: 10
  },
  {
    id: 5,
    product: '阿薩姆奶茶',
    description: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50,
    stock: 25
  },
  {
    id: 6,
    product: '檸檬冰茶',
    description: '檸檬與冰茶的清新組合',
    price: 45,
    stock: 20
  },
  {
    id: 7,
    product: '芒果綠茶',
    description: '芒果與綠茶的獨特風味',
    price: 55,
    stock: 18
  },
  {
    id: 8,
    product: '抹茶拿鐵',
    description: '抹茶與鮮奶的絕配',
    price: 60,
    stock: 20
  }
])

const reduceStock = (item) => {
  if (item.stock > 0) item.stock--
}

const addStock = (item) => {
  item.stock++
}

// 編輯品項
const editItem = ref(null)

const edit = (item) => {
  editItem.value = { ...item }
}

// 確認編輯
const confirmEdit = () => {
  // 找出編輯中的品項
  const modified = menu.value.find((item) => item.id === editItem.value.id)
  // 更新品項資料
  if (modified) {
    modified.product = editItem.value.product
    modified.description = editItem.value.description
    modified.price = editItem.value.price
  }
  editItem.value = null
}

// 取消編輯
const cancelEdit = () => {
  editItem.value = null
}
</script>

<template>
  <table>
    <thead>
      <tr>
        <th>品項</th>
        <th>描述</th>
        <th>價格</th>
        <th>庫存</th>
        <th></th>
      </tr>
    </thead>
    <tbody v-for="item in menu" :key="item.id">
      <tr>
        <td>{{ item.product }}</td>
        <td>
          <small>{{ item.description }}</small>
        </td>
        <td>{{ item.price }}</td>
        <td>
          {{ item.stock }}
          <button
            type="button"
            class="reducebutton"
            @click="reduceStock(item)"
            :disabled="item.stock <= 0"
          >
            -
          </button>
          <button type="button" class="addbutton" @click="addStock(item)">+</button>
        </td>
        <td>
          <button type="button" @click="edit(item)">編輯</button>
        </td>
      </tr>
    </tbody>
  </table>
  <div class="editbox" v-if="editItem">
    <h3>編輯品項</h3>
    <label for="name">品項:</label>
    <input v-model="editItem.product" /><br />
    <label for="description">描述:</label>
    <input v-model="editItem.description" /><br />
    <label for="price">價格:</label>
    <input v-model.number="editItem.price" />
    <div>
      <button type="button" @click="confirmEdit">確認</button>
      <button type="button" @click="cancelEdit">取消</button>
    </div>
  </div>
</template>

<style scoped>
table {
  width: 90%;
  border-collapse: separate;
  border-spacing: 0;
  margin: 10px auto;
}

thead {
  background-color: #333;
  color: #fff;
}

th {
  padding: 5px;
  text-align: center;
  border: 1px solid #444;
}

td {
  padding: 5px;
  text-align: center;
  border: 1px solid #eee;
}

button {
  background-color: #28a745;
  color: #fff;
  border: none;
  padding: 6px 12px;
  cursor: pointer;
  border-radius: 5px;
  font-size: 14px;
}

.reducebutton {
  margin-left: 30px;
}

.addbutton {
  margin-left: 10px;
}

button:disabled {
  background-color: #6c757d;
  cursor: not-allowed;
}

.editbox {
  width: 25%;
  height: 250px;
  margin: 0 auto;
  padding: 15px;
  border: 1px solid black;
}

h3 {
  margin: 0 0 5px 0;
  color: #333;
}

input {
  margin: 5px 0 10px 0;
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 5px;
  width: calc(100% - 16px);
  box-sizing: border-box;
}

div > button {
  margin-right: 12px;
}
</style>
