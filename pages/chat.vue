<template>
    <div class="c-wrap">
        <div class="c-chat">
            <message
               v-for="m in messages" :key="m.text"
               :name="m.name"
               :text="m.text"
               :owner="m.id === user.id"
            />
        </div>
        <div class="c-form">
            <chat-form/>
        </div>
    </div>
</template>

<script>

import {mapState} from 'vuex';
import ChatForm from '../components/ChatForm.vue';
import Message from '../components/Message.vue';

export default {
   layout: "chatLayout",
   components: { Message, ChatForm },
   middleware: ['chat'],
   head() {
       return {
           title: `Комната ${this.user.room}`
       }
   },
   computed: mapState(["user", "messages"])
}
</script>

<style scoped>
   .c-wrap {
       height: 100%;
       position: relative;
       overflow: hidden;
   }

   .c-form {
       position: absolute;
       bottom: 0;
       left: 0;
       right: 0;
       padding: 1rem;
       height: 80px;
       background: #121212;
   }

   .c-chat {
       position: absolute;
       top: 0;
       right: 0;
       left: 0;
       bottom: 80px;
       padding: 1rem;
       overflow-y: auto;
   }
</style>