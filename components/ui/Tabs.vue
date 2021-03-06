<template>
  <div class="tabs">
    <nav class="tabs__nav">
      <ul class="tabs__nav-list">
        <li class="tabs__nav-item" v-for="(tab, index) in tabs" :key="tab.id">
          <button
            @click="activeTab = index"
            :class="[
              'tabs__nav-button',
              mod('tabs__nav-button_theme_'),
              { 'tabs__nav-button_active': activeTab === index },
            ]"
          >
            {{ tab.title }}
          </button>
        </li>
      </ul>
    </nav>
    <transition name="transition-slide" mode="out-in">
      <div class="tabs__tab-content" :key="tabs[activeTab].text">
        <div
          :class="['tabs__tab-paragraph', mod('tabs__tab-paragraph_theme_')]"
          :style="{ minHeight: `${height}px` }"
          v-html="tabs[activeTab].text"
        ></div>
        <slot :name="tabs[activeTab].id"></slot>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  props: {
    tabs: {
      type: Array,
      default: [],
    },
    height: Number,
    theme: String,
  },
  data() {
    return {
      activeTab: 0,
    };
  },
  computed: {
    // Класс модификатор элемента
    mod() {
      return function(element) {
        return [this.theme ? `${element}${this.theme}` : ''];
      };
    },
  },
};
</script>

<style scoped>
.tabs {
  display: flex;
  justify-content: flex-end;
}

@media screen and (max-width: 768px) {
  .tabs {
    flex-direction: column;
    align-items: flex-start;
  }
}

.tabs__nav-list {
  flex-shrink: 0;
  list-style: none;
  margin: 0 40px;
  padding: 0;
}

@media screen and (max-width: 1024px) {
  .tabs__nav-list {
    margin: 0 30px;
  }
}

@media screen and (max-width: 768px) {
  .tabs__nav-list {
    margin: 0 0 24px;
  }
}

@media screen and (max-width: 425px) {
  .tabs__nav-list {
    margin: 0 0 16px;
  }
}

.tabs__nav-item {
  margin: 0 0 10px;
  text-align: right;
}

@media screen and (max-width: 1024px) {
  .tabs__nav-item {
    margin: 0 0 8px;
  }
}

@media screen and (max-width: 768px) {
  .tabs__nav-item {
    display: inline;
    text-align: left;
    margin: 0 30px 0 0;
  }
}
@media screen and (max-width: 425px) {
  .tabs__nav-item {
    margin: 0 16px 0 0;
  }
}

.tabs__nav-item:last-of-type {
  margin: 0;
}

.tabs__nav-button {
  padding: 0;
  border: none;
  border-bottom: 1px solid transparent;
  background: none;
  font-family: 'Inter', Arial, sans-serif;
  font-weight: normal;
  font-style: normal;
  font-size: 18px;
  line-height: 1.3;
  white-space: nowrap;
  color: #666;
  transition: 0.25s;
  cursor: pointer;
  transition: 0.25s;
}

@media screen and (max-width: 1024px) {
  .tabs__nav-button {
    font-size: 15px;
  }
}

@media screen and (max-width: 768px) {
  .tabs__nav-button {
    padding-bottom: 4px;
  }
}

@media screen and (max-width: 425px) {
  .tabs__nav-button {
    font-size: 13px;
  }
}

.tabs__nav-button:focus {
  outline: none;
}

.tabs__nav-button:hover {
  color: #000;
}

@media screen and (max-width: 768px) {
  .tabs__nav-button:hover {
    border-bottom: 2px solid #613a93;
  }
}

.tabs__nav-button_theme_dark {
  color: #dedede;
}

.tabs__nav-button_theme_dark:hover {
  color: rgb(255, 255, 255);
}

@media screen and (max-width: 768px) {
  .tabs__nav-button_theme_dark:hover {
    border-bottom: 2px solid #fff;
  }
}

.tabs__nav-button.tabs__nav-button_active {
  color: #000;
}

@media screen and (max-width: 768px) {
  .tabs__nav-button.tabs__nav-button_active {
    border-bottom: 2px solid #613a93;
  }
}

.tabs__nav-button_theme_dark.tabs__nav-button_active {
  color: #fff;
}

@media screen and (max-width: 768px) {
  .tabs__nav-button_theme_dark.tabs__nav-button_active {
    border-bottom: 2px solid #fff;
  }
}

.tabs__tab-content {
  max-width: 640px;
}

@media screen and (max-width: 1024px) {
  .tabs__tab-content {
    max-width: 640px;
  }
}

@media screen and (max-width: 768px) {
  .tabs__tab-content {
    max-width: 380px;
  }
}

@media screen and (max-width: 425px) {
  .tabs__tab-content {
    max-width: none;
  }
}

.tabs__tab-paragraph {
  font-style: normal;
  font-weight: normal;
  font-size: 18px;
  line-height: 1.22;
  color: #666;
  margin: 0 0 20px;
}

@media screen and (max-width: 1024px) {
  .tabs__tab-paragraph {
    font-size: 15px;
    margin: 0 0 16px;
  }
}

@media screen and (max-width: 425px) {
  .tabs__tab-paragraph {
    font-size: 13px;
    margin: 0 0 16px;
  }
}

.tabs__tab-paragraph:last-of-type {
  margin: 0;
}

.tabs__tab-paragraph_theme_dark {
  color: #dedede;
}

.transition-slide-enter-active,
.transition-slide-leave-active {
  transition: all 0.25s;
}

.transition-slide-enter {
  transform: translateY(-16px);
  opacity: 0;
}

.transition-slide-leave-to {
  transform: translateY(16px);
  opacity: 0;
}
</style>
