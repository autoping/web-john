<template>

<form class="chat-box" @submit.prevent="send">
    <input
        v-model="text"
        placeholder="Текст сообщения"
        type="text"
    />
    <button :disabled="text === ''" type="submit">
        <i class="fa-regular fa-paper-plane fa-2xl"></i>
    </button>
    
</form>

</template>



<script>

import messageService from '@/services/MessageService';

export default {

    name: 'ChatBox',

    props: {
        cardId: String
    },

    data() {
        return {
            text: ''
        }
    },

    methods: {
        async send() {
            const message = await messageService.send(this.cardId, this.text);
            this.$emit('send-message', message);
            this.text = '';
        }
    }
}

</script>



<style scoped>

.chat-box {
    position: fixed;
    bottom: 0;
    width: 100%;
    max-width: 800px;
    display: flex;
}

button {
  border: 0;
  background: #2a60ff;
  color: white;
  cursor: pointer;
  padding: 1rem;
}

input {
  border: 0;
  padding: 1rem;
  background: rgba(0, 0, 0, 0.1);
}

input {
    width:100%;
    flex-grow: 1;
}

input[type="color"],
input[type="date"],
input[type="datetime"],
input[type="datetime-local"],
input[type="email"],
input[type="month"],
input[type="number"],
input[type="password"],
input[type="search"],
input[type="tel"],
input[type="text"],
input[type="time"],
input[type="url"],
input[type="week"],
select:focus,
textarea {
  font-size: 16px;
}

button:disabled {
    opacity: 0.5;
}

</style>
