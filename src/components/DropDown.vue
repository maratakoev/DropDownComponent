<template>
  <div class="drop-down" ref="dropdown">
    <div @click="toggle" class="drop-down__button" tabindex="-1">
      <span :class="{'drop-down__name-active': isOpen, 'drop-down__name-not-active': !isOpen}">
        {{ modelValue || 'Выберите...' }}
      </span>
      <span class="drop-down__icon">
        {{ isOpen ? '▲' : '▼' }} 
      </span>
    </div>
    <transition name="fade">
      <div v-if="isOpen">
        <ul class="drop-down__list">
          <li 
            v-for="(item, index) in items" 
            :key="index" 
            class="drop-down__item"
            @click="selectItem(item)">
            {{ item }}

          </li>
          
        </ul>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  props: {
    items: {
      type: Array,
      required: true,
    },
    modelValue: {
      type: String,
      default: ''
    }
  },
  data() {
    return {
      isOpen: false,
    };
  },
  methods: {
    toggle() {
      this.isOpen = !this.isOpen;
    },
    selectItem(item) {
      this.$emit('update:modelValue', item); // Обновляем v-model в родителе
      this.isOpen = false; // Закрываем список после выбора
    },
    closeDropdown(event) {
      // Проверяем, был ли клик за пределами компонента
      if (this.$refs.dropdown && !this.$refs.dropdown.contains(event.target)) {
        this.isOpen = false;
      }
    },
  },
  mounted() {
    // Добавляем слушатель на документ при монтировании компонента
    document.addEventListener('click', this.closeDropdown);
  },
  beforeDestroy() {
    // Удаляем слушатель при уничтожении компонента
    document.removeEventListener('click', this.closeDropdown);
  }
  
};
</script>

<style scoped>
.drop-down {
  width: 326px;
  height: 58px;
  border-radius: 4px;
  background-color: rgb(231, 229, 229);
  box-sizing: border-box;
}

.drop-down__button {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 20px 14px;
  cursor: pointer;
  color: grey;
  outline: none; /* Убираем подсветку при фокусе */
  -webkit-tap-highlight-color: transparent; /* Убираем подсветку для мобильных */
}
.drop-down__icon {
  z-index: 2;
}

.drop-down__name-not-active {
  z-index: 2;
  font-size: 16px;
  transition: transform 0.3s ease;
  transform: translateY(0);
}

.drop-down__name-active {
  z-index: 2;
  font-size: 16px;
  transition: transform 0.3s ease;
  transform: translateY(-15px); /* Поднимем текст вверх при активации */
}

.drop-down__list {
  width: 326px;
  border-radius: 4px;
  background-color: rgb(231, 229, 229);
  box-sizing: border-box;
  margin-top: -50px;
  padding-left: 0px;
  overflow: hidden;
  outline: none; /* Убираем фокус на списке */
  -webkit-tap-highlight-color: transparent; /* Убираем подсветку для мобильных */
}

.drop-down__item {
  padding: 16px 16px;
  list-style-type: none;
  display: flex;
  outline: none; /* Убираем фокус на элементах списка */
  -webkit-tap-highlight-color: transparent;
  border-bottom: 1px solid grey;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease, max-height 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  max-height: 0;
}

.fade-enter-to,
.fade-leave-from {
  opacity: 1;
  max-height: 300px; /* Устанавливаем максимальную высоту для анимации */
}
</style>
