# **Tutorial Completo Vue.js 3 para Iniciantes**

Este tutorial cobre o básico do Vue.js 3, desde a criação de um projeto até a navegação entre páginas, reatividade, hooks e mais.

## **Sumário**
1. [Introdução ao Vue.js 3](#1-introdução-ao-vuejs-3)
2. [O que é Reatividade?](#2-o-que-é-reatividade)
3. [Como Criar um Projeto Vue.js 3](#3-como-criar-um-projeto-vuejs-3)
4. [Navegação Entre Páginas com Vue Router](#4-navegação-entre-páginas-com-vue-router)
5. [Reatividade no Vue.js](#5-reatividade-no-vuejs)
6. [Comunicação entre Componentes](#6-comunicação-entre-componentes)
7. [Usando v-for, v-if e v-else](#7-usando-v-for-v-if-e-v-else)
8. [Hooks no Vue.js 3](#8-hooks-no-vuejs-3)
9. [Instalar Pacotes com NPM](#9-instalar-pacotes-com-npm)
10. [Remover a Reatividade](#10-remover-a-reatividade)
11. [Passar Props](#11-passar-props)
12. [Conclusão](#12-conclusão)

---

## **1. Introdução ao Vue.js 3**

O Vue.js é um framework JavaScript progressivo usado para construir interfaces de usuário dinâmicas e interativas. É amplamente utilizado para o desenvolvimento de aplicativos da web, pois é simples de adotar e integrar com outras bibliotecas ou projetos existentes. O Vue.js se destaca por sua **reatividade**, que permite a sincronização automática entre o modelo de dados e a interface do usuário. Isso significa que qualquer mudança no estado dos dados refletirá automaticamente na interface.

O Vue.js 3 traz melhorias significativas em termos de desempenho, tamanho de bundle e uma nova API chamada **Composition API**, que torna a organização do código mais flexível e escalável, especialmente em projetos maiores.

---

## **2. O que é Reatividade?**

**Reatividade** no Vue.js é o conceito central que permite que as alterações nos dados de um aplicativo sejam automaticamente refletidas na interface do usuário sem a necessidade de atualizações manuais.

Quando você define uma variável como reativa no Vue.js (usando `ref` ou `reactive`), o framework "escuta" essas mudanças e atualiza a interface toda vez que o valor dessa variável é modificado. Por exemplo, se você tem um contador no seu app e o valor desse contador muda, o Vue.js vai se certificar de que o valor exibido na tela seja atualizado automaticamente, sem que você precise interagir diretamente com o DOM.

No Vue.js, a reatividade é construída sobre a **Programação Reativa**, onde as dependências dos dados são rastreadas para que, sempre que os dados mudem, todas as partes dependentes do código também sejam atualizadas de forma eficiente.

Exemplo de reatividade básica:

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

Neste caso, o Vue.js garante que a interface será atualizada toda vez que `contador.value` mudar.

---

## **3. Como Criar um Projeto Vue.js 3**

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

## **4. Navegação Entre Páginas com Vue Router**

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

## **5. Reatividade no Vue.js**

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

## **6. Comunicação entre Componentes**

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

## **7. Usando v-for, v-if e v-else**

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

## **8. Hooks no Vue.js 3**

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

## **9. Instalar Pacotes com NPM**

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

## **10. Remover a Reatividade**

Use o operador de espalhamento para desativar a reatividade:

```js
const valorNormal = { ...valorReativo };
```

---

## **11. Passar Props**

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

## **12. Conclusão**

Neste tutorial, você aprendeu:
- O que é o Vue.js e reatividade
- Como criar um projeto Vue.js 3
- Navegação entre páginas com Vue Router
- Usar reatividade e comunicação entre componentes
- Trabalhar com `v-for`, `v-if`, `v-else`
- Hooks do ciclo de vida
- Instalar pacotes com NPM
- Passar props e remover reatividade

Próximos passos: explore autenticação, gerenciamento de estado com Vuex, e faça o deploy da sua aplicação Vue.js.
