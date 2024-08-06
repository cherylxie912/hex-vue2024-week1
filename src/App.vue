<script setup>
// import HelloWorld from './components/HelloWorld.vue'
// import TheWelcome from './components/TheWelcome.vue'
import { ref } from "vue";

const menuArray = ref([
  {
    id: "1",
    name: "珍珠奶茶",
    des: "香濃奶茶搭配QQ珍珠",
    price: 50,
    stock: 20,
  },
  {
    id: "2",
    name: "冬瓜檸檬",
    des: "清新冬瓜配上新鮮檸檬",
    price: 45,
    stock: 18,
  },
  {
    id: "3",
    name: "翡翠檸檬",
    des: "綠茶與檸檬的完美結合",
    price: 55,
    stock: 34,
  },
  {
    id: "4",
    name: "四季春茶",
    des: "香醇四季春茶，回甘無比",
    price: 45,
    stock: 10,
  },
  {
    id: "5",
    name: "阿薩姆奶茶",
    des: "阿薩姆紅茶搭配香醇鮮奶",
    price: 50,
    stock: 25,
  },
  {
    id: "6",
    name: "檸檬冰茶",
    des: "檸檬與冰茶的清新組合",
    price: 45,
    stock: 20,
  },
  {
    id: "7",
    name: "芒果綠茶",
    des: "芒果與綠茶的獨特風味",
    price: 55,
    stock: 18,
  },
  {
    id: "8",
    name: "抹茶拿鐵",
    des: "抹茶與鮮奶的絕配	",
    price: 60,
    stock: 20,
  },
]);

const nameEditingId = ref(null);
const stockEditingId = ref(null);

function changeStock(id, stock) {
  menuArray.value = menuArray.value.map((item) => {
    if (item.id === id) {
      item.stock = stock;
      console.log(typeof item.stock);
    }
    return item;
  });
}

function reName(id) {
  if (nameEditingId.value === id) {
    nameEditingId.value = null;
  } else {
    nameEditingId.value = id;
  }
}

function reStock(id) {
  if (stockEditingId.value === id) {
    stockEditingId.value = null;
  } else {
    stockEditingId.value = id;
  }
}
</script>

<template>
  <nav
    class="navbar navbar-expand-lg navbar-dark bg-dark"
    style="background-color: #5c413e !important"
  >
    <div class="container-fluid">
      <a class="navbar-brand fw-bold fs-4" style="color: #ebe0d1" href="#">
        <img
          src="@/assets/title.svg"
          alt=""
          width="45"
          height="36"
          class="d-inline-block align-text-center"
        />
        巴柏沒有踢
      </a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNav"
        aria-controls="navbarNav"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item">
            <a class="nav-link active" aria-current="page" href="#">餐點管理工具</a>
          </li>
          <!-- <li class="nav-item">
            <a class="nav-link" href="#">Features</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">Pricing</a>
          </li>
          <li class="nav-item">
            <a class="nav-link disabled">Disabled</a>
          </li> -->
        </ul>
      </div>
    </div>
  </nav>
  <div id="container" class="container-fluid pt-5">
    <div class="row mt-4">
      <div class="col-1"></div>
      <div class="col">
        <table class="table">
          <thead>
            <tr class="fs-4">
              <th scope="col" class="text-center">品項</th>
              <th scope="col" class="text-center">描述</th>
              <th scope="col" class="text-center">價格<span class="fs-6">/元</span></th>
              <th scope="col" class="text-center">庫存<span class="fs-6">/杯</span></th>
              <th scope="col" class="text-center">操作</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in menuArray" :key="item.id">
              <td class="text-center fs-5">
                <span v-if="nameEditingId !== item.id">{{ item.name }}</span>
                <input
                  v-else
                  type="text"
                  v-model="item.name"
                  @blur="reName(item.id)"
                  style="width: 15ch"
                />
              </td>
              <td class="text-center">
                {{ item.des }}
              </td>
              <td class="text-center fs-5">{{ item.price }}</td>
              <td class="text-center fs-5">
                <button
                  class="btn btn-secondary mx-3"
                  type="button"
                  @click="changeStock(item.id, item.stock - 1)"
                  :disabled="item.stock < 1"
                >
                  -
                </button>
                <!-- <span>{{ item.stock }}</span> -->
                <!-- <input
                  v-model="item.stock"
                  @click=""
                  :disabled="true"
                  type="number"
                  name=""
                  id=""
                /> -->
                <span v-if="stockEditingId !== item.id">{{ item.stock }}</span>
                <input
                  v-else
                  type="number"
                  v-model="item.stock"
                  @blur="reStock(item.id)"
                  style="width: 4ch"
                />
                <button
                  class="btn btn-secondary mx-3"
                  type="button"
                  @click="changeStock(item.id, item.stock + 1)"
                >
                  +
                </button>
              </td>
              <td class="text-center">
                <button
                  class="btn btn-primary ms-3 my-2"
                  type="button"
                  @click="reName(item.id)"
                >
                  {{ nameEditingId === item.id ? "保存編輯" : "編輯品項" }}
                </button>
                <button
                  class="btn btn-success ms-3"
                  type="button"
                  @click="reStock(item.id)"
                >
                  {{ stockEditingId === item.id ? "保存編輯" : "編輯庫存" }}
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
      <div class="col-1"></div>
    </div>
  </div>
</template>

<style scoped>
html,
body {
  height: 100%;
  padding: 0;
  margin: 0;
}

header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}

#container {
  background-repeat: no-repeat;
  background-position: center;
  background-image: url("@/assets/backgroundImg.png");
  background-color: #bf9c6b !important;
  height: 100vh;
}

table {
  width: 100%; /* 確保表格寬度占滿父容器 */
  background: rgba(255, 255, 255, 0.9);
}

th,
td {
  text-align: center; /* 將文字置中對齊 */
}

th:nth-child(1),
td:nth-child(1) {
  width: 22%; /* 品項欄位寬度 */
}

th:nth-child(2),
td:nth-child(2) {
  width: 20%; /* 描述欄位寬度 */
}

th:nth-child(3),
td:nth-child(3) {
  width: 8%; /* 描述欄位寬度 */
}

th:nth-child(4),
td:nth-child(4) {
  width: 25%; /* 描述欄位寬度 */
}

th:nth-child(5),
td:nth-child(5) {
  width: 25%; /* 價格、庫存和操作欄位寬度 */
}
</style>
