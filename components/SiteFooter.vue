<template>
  <footer class="footer">
    <svg
      aria-hidden="true"
      style="position: absolute; width: 0; height: 0; overflow: hidden;"
      version="1.1"
      xmlns="http://www.w3.org/2000/svg"
      xmlns:xlink="http://www.w3.org/1999/xlink"
    >
      <defs>
        <svg id="close" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="#ffffff" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="arcs">
          <circle cx="12" cy="12" r="10"></circle>
          <line x1="15" y1="9" x2="9" y2="15"></line>
          <line x1="9" y1="9" x2="15" y2="15"></line>
        </svg>
        <symbol id="dark-mode" viewBox="2 2 19.369999999999997 20">
          <path d="m 19.9 12.66 a 1 1 0 0 1 0 -1.32 l 1.28 -1.44 a 1 1 0 0 0 0.12 -1.17 l -2 -3.46 a 1 1 0 0 0 -1.07 -0.48 l -1.88 0.38 a 1 1 0 0 1 -1.15 -0.66 l -0.61 -1.83 a 1 1 0 0 0 -0.95 -0.68 h -4 a 1 1 0 0 0 -1 0.68 l -0.56 1.83 a 1 1 0 0 1 -1.15 0.66 l -1.93 -0.38 a 1 1 0 0 0 -1 0.48 l -2 3.46 a 1 1 0 0 0 0.1 1.17 l 1.27 1.44 a 1 1 0 0 1 0 1.32 l -1.27 1.44 a 1 1 0 0 0 -0.1 1.17 l 2 3.46 a 1 1 0 0 0 1.07 0.48 l 1.88 -0.38 a 1 1 0 0 1 1.15 0.66 l 0.61 1.83 a 1 1 0 0 0 1 0.68 h 4 a 1 1 0 0 0 0.95 -0.68 l 0.61 -1.83 a 1 1 0 0 1 1.15 -0.66 l 1.88 0.38 a 1 1 0 0 0 1.07 -0.48 l 2 -3.46 a 1 1 0 0 0 -0.12 -1.17 z m -1.49 1.34 l 0.8 0.9 l -1.28 2.22 l -1.18 -0.24 a 3 3 0 0 0 -3.45 2 l -0.38 1.12 h -2.56 l -0.36 -1.14 a 3 3 0 0 0 -3.45 -2 l -1.18 0.24 l -1.3 -2.21 l 0.8 -0.9 a 3 3 0 0 0 0 -4 l -0.8 -0.9 l 1.28 -2.2 l 1.18 0.24 a 3 3 0 0 0 3.45 -2 l 0.38 -1.13 h 2.56 l 0.38 1.14 a 3 3 0 0 0 3.45 2 l 1.18 -0.24 l 1.28 2.22 l -0.8 0.9 a 3 3 0 0 0 0 3.98 z m -6.77 -6 a 4 4 0 1 0 4 4 a 4 4 0 0 0 -4 -4 z m 0 6 a 2 2 0 1 1 2 -2 a 2 2 0 0 1 -2 2 z"/>
        </symbol>
        <symbol id="twitter" viewBox="0 0 32 32">
          <title>Abrir en nueva ventana Red social Twitter</title>
          <path
            d="M32 7.075c-1.175 0.525-2.444 0.875-3.769 1.031 1.356-0.813 2.394-2.1 2.887-3.631-1.269 0.75-2.675 1.3-4.169 1.594-1.2-1.275-2.906-2.069-4.794-2.069-3.625 0-6.563 2.938-6.563 6.563 0 0.512 0.056 1.012 0.169 1.494-5.456-0.275-10.294-2.888-13.531-6.862-0.563 0.969-0.887 2.1-0.887 3.3 0 2.275 1.156 4.287 2.919 5.463-1.075-0.031-2.087-0.331-2.975-0.819 0 0.025 0 0.056 0 0.081 0 3.181 2.263 5.838 5.269 6.437-0.55 0.15-1.131 0.231-1.731 0.231-0.425 0-0.831-0.044-1.237-0.119 0.838 2.606 3.263 4.506 6.131 4.563-2.25 1.762-5.075 2.813-8.156 2.813-0.531 0-1.050-0.031-1.569-0.094 2.913 1.869 6.362 2.95 10.069 2.95 12.075 0 18.681-10.006 18.681-18.681 0-0.287-0.006-0.569-0.019-0.85 1.281-0.919 2.394-2.075 3.275-3.394z"
          />
        </symbol>
        <symbol id="github" viewBox="0 0 32 32">
          <title>Abrir en nueva ventana cuenta de Github</title>
          <path
            d="M16 0.395c-8.836 0-16 7.163-16 16 0 7.069 4.585 13.067 10.942 15.182 0.8 0.148 1.094-0.347 1.094-0.77 0-0.381-0.015-1.642-0.022-2.979-4.452 0.968-5.391-1.888-5.391-1.888-0.728-1.849-1.776-2.341-1.776-2.341-1.452-0.993 0.11-0.973 0.11-0.973 1.606 0.113 2.452 1.649 2.452 1.649 1.427 2.446 3.743 1.739 4.656 1.33 0.143-1.034 0.558-1.74 1.016-2.14-3.554-0.404-7.29-1.777-7.29-7.907 0-1.747 0.625-3.174 1.649-4.295-0.166-0.403-0.714-2.030 0.155-4.234 0 0 1.344-0.43 4.401 1.64 1.276-0.355 2.645-0.532 4.005-0.539 1.359 0.006 2.729 0.184 4.008 0.539 3.054-2.070 4.395-1.64 4.395-1.64 0.871 2.204 0.323 3.831 0.157 4.234 1.026 1.12 1.647 2.548 1.647 4.295 0 6.145-3.743 7.498-7.306 7.895 0.574 0.497 1.085 1.47 1.085 2.963 0 2.141-0.019 3.864-0.019 4.391 0 0.426 0.288 0.925 1.099 0.768 6.354-2.118 10.933-8.113 10.933-15.18 0-8.837-7.164-16-16-16z"
          />
        </symbol>
        <symbol id="linkedin" viewBox="0 0 32 32">
          <title>Abrir en nueva ventana Red profesional Linkedin</title>
          <path
            d="M12 12h5.535v2.837h0.079c0.77-1.381 2.655-2.837 5.464-2.837 5.842 0 6.922 3.637 6.922 8.367v9.633h-5.769v-8.54c0-2.037-0.042-4.657-3.001-4.657-3.005 0-3.463 2.218-3.463 4.509v8.688h-5.767v-18z"
          />
          <path d="M2 12h6v18h-6v-18z" />
          <path d="M8 7c0 1.657-1.343 3-3 3s-3-1.343-3-3c0-1.657 1.343-3 3-3s3 1.343 3 3z" />
        </symbol>
        <symbol id="codepen" viewBox="0 0 32 32">
          <title>Abrir en nueva ventana Perfil en Codepen</title>
          <path
            d="M29.555 11.501l-14-9.333c-0.336-0.224-0.774-0.224-1.109 0l-14 9.333c-0.278 0.185-0.445 0.498-0.445 0.832v9.333c0 0.334 0.167 0.647 0.445 0.832l14 9.333c0.168 0.112 0.361 0.168 0.555 0.168s0.387-0.056 0.555-0.168l14-9.333c0.278-0.185 0.445-0.498 0.445-0.832v-9.333c0-0.334-0.167-0.647-0.445-0.832zM15 20.465l-5.197-3.465 5.197-3.465 5.197 3.465-5.197 3.465zM16 11.798v-6.93l11.197 7.465-5.197 3.465-6-4zM14 11.798l-6 4-5.197-3.465 11.197-7.465v6.93zM6.197 17l-4.197 2.798v-5.596l4.197 2.798zM8 18.202l6 4v6.93l-11.197-7.465 5.197-3.465zM16 22.202l6-4 5.197 3.465-11.197 7.465v-6.93zM23.803 17l4.197-2.798v5.596l-4.197-2.798z"
          />
        </symbol>
      </defs>
    </svg>
    <div class="footer__social">
      <div v-for="social in socials" :key="social.link">
        <a :href="social.link" target="_blank" :aria-label="social.label" rel="noopener">
          <svg class="svg-icon">
            <use :xlink:href="social.icon" />
          </svg>
        </a>
      </div>
    </div>
    <div class="footer__copy">
      <p>Iván Albizu</p>
      <a href="https://vuejs.org/" rel="noopener" target="_blank">Vuejs</a> +
      <a href="https://nuxtjs.org/" rel="noopener" target="_blank">Nuxtjs</a>
    </div>
  </footer>
</template>

<script>
export default {
  data() {
    return {
      socials: [
        { link: "https://github.com/ivanalbizu", icon: "#github", label: "Perfil en Github" },
        { link: "https://twitter.com/ivan_albizu", icon: "#twitter", label: "Perfil en Twitter" },
        { link: "https://www.linkedin.com/in/ivanalbizu/", icon: "#linkedin", label: "Perfil en Linkedin" },
        { link: "http://codepen.io/ivan_albizu", icon: "#codepen", label: "Perfil en Codepen" }
      ]
    };
  }
};
</script>

<style lang="scss">
.footer {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  align-items: center;
  text-align: center;
  &__social {
    display: flex;
    justify-content: center;
    margin-bottom: 3rem;
    & > div {
      padding: 0 1rem;
    }
  }
}
.svg-icon {
  width: 32px;
  height: 32px;
  fill: var(--primary);
  transition: fill 0.2s ease-out;
  &:hover,
  &:focus {
    fill: var(--link-hover);
    transition: fill 0.15s ease-out;
  }
}
</style>
