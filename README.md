# **Tutorial Completo Vue.js 3 para Iniciantes**

Este tutorial cobre o básico do Vue.js 3, desde a criação de um projeto até a navegação entre páginas, reatividade, hooks e mais.

## **Sumário**
1. [Introdução ao Vue.js 3](#1-introdução-ao-vuejs-3)
2. [Como Criar um Projeto Vue.js 3](#2-como-criar-um-projeto-vuejs-3)
3. [Navegação Entre Páginas com Vue Router](#3-navegação-entre-páginas-com-vue-router)
4. [Reatividade no Vue.js](#4-reatividade-no-vuejs)
5. [Comunicação entre Componentes](#5-comunicação-entre-componentes)
6. [Usando v-for, v-if e v-else](#6-usando-v-for-v-if-e-v-else)
7. [Hooks no Vue.js 3](#7-hooks-no-vuejs-3)
8. [Instalar Pacotes com NPM](#8-instalar-pacotes-com-npm)
9. [Remover a Reatividade](#9-remover-a-reatividade)
10. [Passar Props](#10-passar-props)
11. [Conclusão](#11-conclusão)

---

## **1. Introdução ao Vue.js 3**
Vue.js é um framework JavaScript progressivo para a construção de interfaces de usuário. Ele oferece reatividade, sistema de componentes, hooks de ciclo de vida e muito mais.

---

## **2. Como Criar um Projeto Vue.js 3**

### **Comando para criar o projeto:**

```bash
npm init vue@latest
```

Siga as instruções para configurar seu projeto. Após a configuração, rode o projeto:

```bash
cd nome-do-projeto
npm install
npm run dev
```

Acesse o projeto em `http://localhost:3000`.

---

## **3. Navegação Entre Páginas com Vue Router**

Instale o Vue Router:

```bash
npm install vue-router@4
```

Crie o arquivo de rotas `src/router/index.js`:

```js
import { createRouter, createWebHistory } from 'vue-router';
import Home from '../views/Home.vue';
import About from '../views/About.vue';

const routes = [
  { path: '/', component: Home },
  { path: '/about', component: About }
];

const router = createRouter({
  history: createWebHistory(),
  routes
});

export default router;
```

Configure o router em `main.js`:

```js
import { createApp } from 'vue';
import App from './App.vue';
import router from './router';

createApp(App).use(router).mount('#app');
```

Use o `<router-link>` para navegar:

```html
<router-link to="/">Home</router-link>
<router-link to="/about">About</router-link>
<router-view></router-view>
```

---

## **4. Reatividade no Vue.js**

Crie variáveis reativas com `ref`:

```js
import { ref } from 'vue';

export default {
  setup() {
    const contador = ref(0);

    function incrementar() {
      contador.value++;
    }

    return { contador, incrementar };
  }
};
```

Utilize no template:

```html
<button @click="incrementar">Contador: {{ contador }}</button>
```

---

## **5. Comunicação entre Componentes**

### **Chamar função no componente filho:**

Pai:

```html
<ChildComponent @eventoDoFilho="funcaoNoPai" />
```

```js
export default {
  methods: {
    funcaoNoPai() {
      console.log('Função chamada pelo componente filho');
    }
  }
};
```

Filho:

```html
<button @click="$emit('eventoDoFilho')">Chamar Pai</button>
```

---

## **6. Usando v-for, v-if e v-else**

### **Usando v-for:**

```html
<ul>
  <li v-for="item in items" :key="item.id">{{ item.name }}</li>
</ul>
```

### **Usando v-if e v-else:**

```html
<p v-if="mostrar">Este texto será mostrado.</p>
<p v-else>Este texto será mostrado se a condição for falsa.</p>
```

---

## **7. Hooks no Vue.js 3**

### **onMounted:**

```js
import { onMounted } from 'vue';

export default {
  setup() {
    onMounted(() => {
      console.log('Componente montado!');
    });
  }
};
```

### **onBeforeMount:**

```js
import { onBeforeMount } from 'vue';

export default {
  setup() {
    onBeforeMount(() => {
      console.log('Antes de montar o componente');
    });
  }
};
```

### **onUpdated:**

```js
import { onUpdated } from 'vue';

export default {
  setup() {
    onUpdated(() => {
      console.log('Componente atualizado!');
    });
  }
};
```

### **onUnmounted:**

```js
import { onUnmounted } from 'vue';

export default {
  setup() {
    onUnmounted(() => {
      console.log('Componente desmontado!');
    });
  }
};
```

### **watch:**

```js
import { ref, watch } from 'vue';

export default {
  setup() {
    const contador = ref(0);

    watch(contador, (novoValor, valorAntigo) => {
      console.log(`Contador mudou de ${valorAntigo} para ${novoValor}`);
    });

    return { contador };
  }
};
```

### **watchEffect:**

```js
import { ref, watchEffect } from 'vue';

export default {
  setup() {
    const contador = ref(0);

    watchEffect(() => {
      console.log(`Contador atual: ${contador.value}`);
    });

    return { contador };
  }
};
```

---

## **8. Instalar Pacotes com NPM**

Para instalar pacotes adicionais:

```bash
npm install axios
```

Usando o pacote no componente:

```js
import axios from 'axios';

axios.get('https://api.example.com').then(response => {
  console.log(response.data);
});
```

---

## **9. Remover a Reatividade**

Use o operador de espalhamento para desativar a reatividade:

```js
const valorNormal = { ...valorReativo };
```

---

## **10. Passar Props**

Pai:

```html
<Filho :mensagem="mensagemDoPai" />
```

Filho:

```html
<p>{{ mensagem }}</p>
```

```js
export default {
  props: ['mensagem']
};
```

---

## **11. Conclusão**

Neste tutorial, você aprendeu:
- Como criar um projeto Vue.js 3
- Navegação entre páginas com Vue Router
- Usar reatividade e comunicação entre componentes
- Trabalhar com `v-for`, `v-if`, `v-else`
- Hooks do ciclo de vida
- Instalar pacotes com NPM
- Passar props e remover reatividade

Próximos passos: explore autenticação, gerenciamento de estado com Vuex, e faça o deploy da sua aplicação Vue.js.
