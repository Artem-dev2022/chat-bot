<script>
import widgetMessage from './widgetMessage.vue';
import loader from './loaderTyping.vue'

export default {
    components: {widgetMessage, loader},
    data() {
        return {
            messages: [
                {role: 'bot', text: 'Привет! Что я могу для Вас сделать?'},
                {role: 'bot', isLast: true, actions: [
                    {action: 'Заказать пиццу'},
                    {action: 'Установить будильник'},
                    {action: 'Вывести погоду'},
                ]},
            ],
            loader: false
        }
    },
    methods:{
        addMessage(action, last){
            if (!last) return
            this.messages.at(-1).isLast = false;
            this.messages.push({role: 'user', text: action})
            let caseWord;
            switch (action) {
                case 'Заказать пиццу':
                    caseWord = 'заказажу пиццу'
                    break
                case 'Установить будильник':
                    caseWord = 'установлю будильник'
                    break
                case 'Вывести погоду':
                    caseWord = 'выведу погоду'
            }
            const answer = `Хорошо, я ${caseWord}. Что еще могу сделать?`
            const widget = document.querySelector('.widget')
            this.loader = true

            function scrollTimeout(s){
                setTimeout(() => {
                    widget.scrollTo(0, widget.scrollHeight, { behavior: "smooth" })
                }, s)
            }
            scrollTimeout(0)
            setTimeout(() => {
                this.loader = false
                this.messages.push({role: 'bot', text: answer})
            }, 1500);
            setTimeout(() => {
                this.loader = true
            }, 1500)
            scrollTimeout(1500)
            setTimeout(() => {
                this.loader = false
                this.messages.push({role: 'bot', isLast: true, actions: [
                    {action: 'Заказать пиццу'},
                    {action: 'Установить будильник'},
                    {action: 'Вывести погоду'},
                ]})
            }, 2500)
            scrollTimeout(2500)
        }
    }
}
</script>

<template>
    <ul class="widget">
        <li v-for="message, idx in messages" :key="idx" :class="{'user-message': messages[idx].role === 'user', 'bot-message': messages[idx].role === 'bot'}">
            <widgetMessage v-if="messages[idx].text">{{ messages[idx].text }}</widgetMessage> 
            <div v-if="messages[idx].actions" class="actions">
                <widgetMessage v-for="action in messages[idx].actions" 
                    @click="addMessage(action.action, message.isLast)"
                    :class="{'active-btn': messages[idx].isLast}"
                >
                    {{ action.action }}
                </widgetMessage>
            </div>
        </li>
        <loader v-show="loader"/>
    </ul>
</template>

<style scoped>
.widget {
    display: flex;
    flex-direction: column;
    gap: 5px;
    padding: 20px;
    width: 500px;
    height: 500px;
    background: linear-gradient(225deg, #78AC89 0%, #C9D49F 52.28%, #78AC89 96.80%);
    border-radius: 20px;
    overflow: hidden;
    overflow-y: scroll;
}
.widget__list {
    display: flex;
    flex-direction: column;
    gap: 5px;
}
.actions {
    display: flex;
    flex-direction: column;
    gap: 5px;
    width: 100%;
}
.user-message {
    align-self: flex-end;
    width: 100%;
    animation: showForUser 0.2s ease-in;
}
.user-message .message {
    margin: 0 0 auto auto;
    background-color: #E9F5E9;
}
.active-btn {
    cursor: pointer;
    transition: all 0.15s;
}
.active-btn:hover {
    background-color: #d7e6eb;
}
.bot-message {
    animation: showForBot 0.2s ease-in;
}
@keyframes showForBot {
    0% {
        opacity: 0;
        transform: translateX(-30px);
    }
    100% {
        opacity: 1;
        transform: translateX(0px);
    }
}
@keyframes showForUser {
    0% {
        opacity: 0;
        transform: translateX(30px);
    }
    100% {
        opacity: 1;
        transform: translateX(0px);
    }
}
</style>