<template>
  <div id="app" :style="{ backgroundColor: isBlackBackground ? '#000' : '#fff', color: isBlackBackground ? '#fff' : '#000' }">
    <button @click="toggleBackgroundColor" class="toggle">Toggle Background Color</button>

    <div class="chat-container">
      <div class="chat-widget">
        <div v-for="message in messages" :key="message.id" class="message">
          <p :class="{'user-message': message.from === 'user', 'bot-message': message.from === 'bot'}">{{message.text}}</p>
        </div>
      </div>
      <div class="input-container">
        <input v-model="userInput" @keyup.enter="sendMessage" placeholder="Введите сообщение..." class="input" />
        <button @click="sendMessage" :disabled="userInput.trim() === ''" class="send">Отправить</button>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  data() {
    return {
      messages: [
        { id: 1, from: 'bot', text: 'Привет! Что я могу для Вас сделать?' }
      ],
      userInput: '',
      isBlackBackground: false
    };
  },
  methods: {
    sendMessage() {
      const userMessage = this.userInput.trim();
      if (userMessage === '') return;

     
      this.messages.push({ id: this.messages.length + 1, from: 'user', text: userMessage });

      
      const botResponse = this.generateBotResponse(userMessage);

      
      this.messages.push({ id: this.messages.length + 1, from: 'bot', text: botResponse });

       
      this.userInput = '';
    },
    generateBotResponse(userMessage) {
  

  
  if (userMessage.toLowerCase().includes('погода')) {
    
    const todayWeather = 'солнечно';
    return `Бот: Сегодня ${todayWeather}, через 5 дней ожидается дождь.`;
  } else if (userMessage.toLowerCase().includes('новости')) {
    
    return 'Бот: В мире произошли важные события, следите за новостями на новостных порталах.';
  } else if (userMessage.toLowerCase().includes('спорт')) {
    
    return 'Бот: Лучший спортивный результат - это здоровый образ жизни!';
  } else if (userMessage.toLowerCase().includes('здоровье')) {
    
    return 'Бот: Заботьтесь о своем здоровье, регулярные занятия физической активностью помогут вам чувствовать себя лучше.';
  } else if (userMessage.toLowerCase().includes('технологии')) {
   
    return 'Бот: Технологии развиваются быстро, следите за последними трендами и новинками в мире технологий.';
  } else if (userMessage.toLowerCase().includes('искусство')) {
    
    return 'Бот: Искусство вдохновляет, посещайте галереи и выставки, чтобы насладиться красотой творчества.';
  } else if (userMessage.toLowerCase().includes('путешествия')) {
   
    return 'Бот: Путешествия расширяют горизонты, планируйте свои приключения и открывайте новые места.';
  } else if (userMessage.toLowerCase().includes('образование')) {
    
    return 'Бот: Образование важно, постоянно развивайте свои знания и умения.';
  } else if (userMessage.toLowerCase().includes('любовь')) {
    
    return 'Бот: Любовь — это сила, способная изменить мир, цените и берегите своих близких.';
  } else if (userMessage.toLowerCase().includes('кулинария')) {
   
    return 'Бот: Экспериментируйте с кулинарией, готовьте разнообразные блюда и наслаждайтесь кулинарными шедеврами.';
  } else if (userMessage.toLowerCase().includes('музыка')) {
    
    return 'Бот: Музыка — это язык души, наслаждайтесь разнообразием музыкальных жанров.';
  } else {
    
    return `Бот: ${userMessage}`;
  }
},

    toggleBackgroundColor() {
      this.isBlackBackground = !this.isBlackBackground;
    },
  },
};
</script>

<style>
.input {
  border-radius: 10px;
  padding: 8px; /* Увеличенный отступ для лучшего визуального восприятия */
  margin-bottom: 10px;
  border: 1px solid #ccc; /* Добавлен бордер для четкости */
  outline: none; /* Убрана рамка фокуса */
}

.send {
  color: white;
  background-color: #3f51b5;
  border-radius: 10px;
  padding: 8px; /* Увеличенный отступ для лучшего визуального восприятия */
  outline: none;
  box-shadow: none;
  margin-left: 10px;
}

.toggle {
  color: black;
  background-color: aliceblue;
  padding: 5px;
  border-radius: 8px;
  outline: none;
  box-shadow: none;
  border: 1px solid #ccc; /* Добавлен бордер для четкости */
}

/* Стили для прокрутки чата */
.chat-widget {
  border: 1px solid #ccc;
  border-radius: 10px;
  padding: 10px;
  margin-bottom: 20px;
  max-width: 300px;
  overflow-y: auto; /* Используем автоматическую прокрутку */
  height: 200px;
}

/* Остальные стили без изменений */
.chat-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
}

.user-message {
  background-color: #009688;
  color: white;
  border-radius: 10px;
  padding: 10px;
  margin-bottom: 10px;
  max-width: 200px;
  word-wrap: break-word;
}

.bot-message {
  background-color: #3f51b5;
  color: white;
  border-radius: 10px;
  padding: 10px;
  margin-bottom: 10px;
  max-width: 200px;
  word-wrap: break-word;
}
/* Добавляем стили для скролла */
.chat-widget::-webkit-scrollbar {
  width: 10px; /* Ширина полосы прокрутки */
}

.chat-widget::-webkit-scrollbar-thumb {
  background-color: #E8E8E8; /* Цвет ползунка */
  border-radius: 5px; /* Скругление углов ползунка */
}

/* Дополнительные стили для скролла при наведении на ползунок */
.chat-widget::-webkit-scrollbar-thumb:hover {
  background-color: #555; /* Измененный цвет ползунка при наведении */
}

.send:hover,
.toggle:hover {
  background-color: #2c3e50; /* Новый цвет фона при ховере */
  color: #fff; /* Новый цвет текста при ховере */
}
</style>