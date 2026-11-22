<template>
  <div id="app">
    <button class="theme-toggle" type="button" @click="toggleTheme" :aria-label="'Trocar para tema ' + (isDark ? 'claro' : 'escuro')">
      {{ isDark ? '☀️ Claro' : '🌙 Escuro' }}
    </button>
    <h1>Currency Converter</h1>
    <div class="line">
    <Converter currA="USD" currB="BRL"></Converter>
    <Converter currA="BRL" currB="USD"></Converter>
    </div>
    <div class="line">
    <Converter currA="CAD" currB="BRL"></Converter>
    <Converter currA="BRL" currB="CAD"></Converter>
    </div>
    <div class="line">
    <Converter currA="EUR" currB="BRL"></Converter>
    <Converter currA="BRL" currB="EUR"></Converter>
    </div>
    <footer class="footerStyle">
      <a href="https://gabrieldmonteiro.com.br" target="blank">gabrieldmonteiro.com.br</a>
    </footer>
  </div>
</template>

<script>

import Converter from "./components/Converter.vue";

const THEME_KEY = "theme";

export default {
  name: 'app',
  components: {
    Converter
  },
  data() {
    return {
      theme: localStorage.getItem(THEME_KEY) || "dark"
    };
  },
  computed: {
    isDark() {
      return this.theme === "dark";
    }
  },
  watch: {
    theme: {
      immediate: true,
      handler(value) {
        document.documentElement.setAttribute("data-theme", value);
        localStorage.setItem(THEME_KEY, value);
      }
    }
  },
  methods: {
    toggleTheme() {
      this.theme = this.isDark ? "light" : "dark";
    }
  }
};

</script>

<style>
:root {
  --bg: #f5f7fa;
  --text: #2c3e50;
  --card-bg: #ffffff;
  --input-bg: #ffffff;
  --border: #d0d7de;
  --shadow: rgba(0, 0, 0, 0.15);
  --accent: #3b82f6;
  --accent-hover: #2563eb;
  color-scheme: light;
}

:root[data-theme="dark"] {
  --bg: #0f1117;
  --text: #e6e8ee;
  --card-bg: #1a1d27;
  --input-bg: #232734;
  --border: #353b4d;
  --shadow: rgba(0, 0, 0, 0.6);
  --accent: #6366f1;
  --accent-hover: #4f46e5;
  color-scheme: dark;
}

body {
  margin: 0;
  background: var(--bg);
  transition: background 0.2s ease;
}

#app {
  max-width: 900px;
  margin: auto;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: var(--text);
  padding: 0 16px;
  margin-top: 60px;
  position: relative;
}

.theme-toggle {
  position: absolute;
  top: -40px;
  right: 16px;
  padding: 6px 12px;
  border-radius: 6px;
  border: 1px solid var(--border);
  background: var(--card-bg);
  color: var(--text);
  cursor: pointer;
  font-size: 13px;
}

.line{
  margin-top: 40px;
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
  gap: 16px;
}

.footerStyle{
  margin-top: 20px;
  text-align: right;
  font-size: 9px;
}

.footerStyle a {
  color: var(--text);
  opacity: 0.7;
}

</style>
