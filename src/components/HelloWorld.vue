<script setup lang="ts">
import { ref } from 'vue'
import * as signalR from '@microsoft/signalr';

defineProps<{ msg: string }>()

const connection = new signalR.HubConnectionBuilder()
  .withUrl("/lab-hub")
  .build();

connection.start().catch(err => console.error(err.toString()));

const Sender = ref("TheAutomaTom");
const Outbound= ref("Can you hear me, now?");
const Conversation= ref(["...", "...", "..."]);

const Send =()=> {
  connection.invoke("SendMessage", User.value, Outbound.value)
    .catch(err => console.error(err.toString()));
}

connection.on("ReceiveMessage", (user, message) => {
  Conversation.value = [...Conversation.value, `${user}:${message}`]
});

</script>

<template>
  <h1>{{ msg }}</h1>

  <div class="card">
    
    <hr/> <!-- =========================== -->
    <h2>Input</h2>
    <h3>
      Username: 
      <input
        v-model="Sender"
      />
    </h3>
    <h3>
      Message: 
      <input
      v-model="Outbound"
      />
    </h3>
    <button
      style="margin-bottom:2em; width:100%"
      @Click="Send()"
    >Send</button>
    
    <hr/> <!-- =========================== -->
    <h2>Output</h2>
    <p
      v-for="(entry, index) in Conversation"
      :key="index"
    >{{entry}}</p>



    
  </div>

</template>

<style scoped>
</style>
