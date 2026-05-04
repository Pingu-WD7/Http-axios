<script setup lang="ts">
import axios from "axios";
import { ref } from "vue";

const lista = ref([] as any[]);

async function loadLista() {
  const response = await axios.get(
    "https://jsonplaceholder.typicode.com/posts",
  );
  lista.value = response.data;
}
</script>

<template>
  <div class="Conteiner">
    <div class="row">
      <div class="col">
        <button class="btn btn-primary" @click="loadLista">
          Carregar Lista
        </button>
        <table class="table">
          <thead>
            <tr>
              <th>Id de usuario</th>
              <th>id titulo</th>
              <th>titulo</th>
              <th>post</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in lista" :key="item.id">
              <td>{{ item.userId }}</td>
              <td>{{ item.id }}</td>
              <td>{{ item.title }}</td>
              <td>{{ item.body }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
