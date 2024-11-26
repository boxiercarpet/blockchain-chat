<script setup>
import { ref } from "vue";
import { my_project_backend } from "declarations/my_project_backend/index";
let chat = ref([]);

async function getChats() {
  chat.value = await my_project_backend.get_chat();
}

async function handleSubmit(e) {
  e.preventDefault();
  const target = e.target;
  const chat = target.querySelector("#chat").value;
  await my_project_backend.save_chat(chat);
  await getChats();
}

getChats();
</script>

<template>
  <main>
    <img src="/logo2.svg" alt="DFINITY logo" />
    <br />
    <br />
    <form action="#" @submit="handleSubmit">
      <label for="chat">Enter your msg: &nbsp;</label>
      <input id="chat" alt="Chat" type="text" />
      <button type="submit">Click Me!</button>
    </form>
    <section id="greeting">
      <div v-for="item in chat">
        {{ item }}
      </div>
    </section>
  </main>
</template>
