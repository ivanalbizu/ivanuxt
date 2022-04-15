<template>
  <div>
    <button class="btn-color-mode" type="button" @click="toggleColorMode">
      <svg class="svg-mode">
        <title>Abrir opciones de configuración visual de la web</title>
        <use xlink:href="#dark-mode" />
      </svg>
    </button>
    <div class="overlay-color-mode-picker">
      <button type="button" @click="toggleColorMode">
        <svg class="svg-icon">
        <title>Cerrar opciones de configuración visual de la web</title>
          <use xlink:href="#close" />
        </svg>
      </button>
      <label v-for="color of colors" :key="color" :for="color" name="color-mode">
        <input :id="color" :checked="$colorMode.preference == color ? true : false" type="radio" @click="$colorMode.preference = color" />
        <span>{{ color }}</span>
      </label>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      colors: ['system', 'dark', 'yellow','light']
    }
  },
  methods: {
    toggleColorMode() {
      document.documentElement.classList.toggle('picker-open')
    }
  },
}
</script>

<style lang="scss">
button {
  -webkit-appearance: none;
  appearance: none;
  background: none;
  border: 0;
  padding: 0;
  cursor: pointer;
}
.btn-color-mode {
  display: flex;
  align-items: center;
}
.picker-open {
  overflow: hidden;
  .overlay-color-mode-picker {
    display: flex;
  }
}
.overlay-color-mode-picker {
  display: none;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  z-index: 1;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  gap: 2rem;
  backdrop-filter: blur(11px);
  background-color:rgba(0,0,0,.3);

  label {
    width: 200px;
    text-align: center;
  }
  input[type="radio"] {
    position: absolute;
    opacity: 0;
  }

  input[type="radio"] {
    + span {
      color: #fff;
      display: block;
      padding: 2rem;
      outline: 1px solid #fff;
      background-color: #000;
    }
    &:checked + span {
      outline-width: 4px;
    }
    &:not(:checked) + span {
      cursor: pointer;
    }
  }
}
.svg-mode {
  width: clamp(1.5rem, 2vw, 3rem);
  height: clamp(1.5rem, 2vw, 3rem);
  fill: var(--primary);
  transition: fill 0.2s ease-out;
  &:hover,
  &:focus {
    fill: var(--link-hover);
    transition: fill 0.15s ease-out;
  }
}
</style>
