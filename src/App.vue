<script setup lang="ts">
import { onMounted, ref } from "vue";
import type Post from "./models/Post";
import http from "./http";

const posts = ref([] as Post[]);

const post = ref({} as Post);

onMounted(listarPost);

async function listarPost() {
  const response = await http.get("/posts");
  posts.value = response.data;
}

async function cadastrarPost() {
  const response = await http.post("/posts", post.value);
  if (response.status < 300) {
    post.value = {} as Post;
    alert("Post cadastrado com sucesso");
  }
}
</script>

<template>
  <div class="container">
    <div class="row">
      <div class="col">
        <form @submit.prevent="cadastrarPost">
          <div class="mb-3">
            <label class="form-label">Id Usuário</label>
            <input class="form-control" type="number" v-model="post.userId" />
          </div>
          <div class="mb-3">
            <label class="form-label">Id</label>
            <input class="form-control" type="number" v-model="post.id" />
          </div>
          <div class="mb-3">
            <label class="form-label">Título</label>
            <input class="form-control" type="text" v-model="post.title" />
          </div>
          <div class="mb-3">
            <label class="form-label">Descrição</label>
            <input class="form-control" type="text" v-model="post.body" />
          </div>
          <button class="btn btn-primary" type="submit">Salvar</button>
        </form>
      </div>
    </div>
    <table class="table">
      <thead>
        <tr>
          <th>User id</th>
          <th>Id</th>
          <th>Título</th>
          <th>Descrição</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="p in posts" :key="p.id">
          <td>{{ p.userId }}</td>
          <td>{{ p.id }}</td>
          <td>{{ p.title }}</td>
          <td>{{ p.body }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped></style>
