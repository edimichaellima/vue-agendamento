# Frontend - Sistema de Agendamento de Transferências

Este é o frontend da aplicação de agendamento de transferências financeiras, desenvolvido com Vue.js 3 e Vite. Ele consome a API REST do backend em Spring Boot e permite agendar transferências e consultar extratos.

---

## 🧱 Arquitetura

- SPA (Single Page Application) com Vue.js 3
- Estrutura em componentes:
  - `AgendarTransferencia.vue`: formulário para agendamento
  - `ListaTransferencias.vue`: tabela com agendamentos
- Camada de serviço isolada (`axios`) para comunicação com a API
- View principal (`Home.vue`) que compõe os componentes

---

## 🚀 Tecnologias e Ferramentas

- **Vue.js 3**
- **Vite**
- **Axios**
- **JavaScript (ES6+)**
- **Node.js 18+**
- **NPM**
- *(Opcional)* Tailwind CSS ou Bootstrap

---

## 📦 Estrutura do projeto

```
vue-agendamento/
├── src/
│   ├── components/
│   │   ├── AgendarTransferencia.vue
│   │   └── ListaTransferencias.vue
│   ├── services/
│   │   └── api.js
│   ├── views/
│   │   └── Home.vue
│   ├── App.vue
│   └── main.js
├── index.html
└── package.json
```

---

## ⚙️ Pré-requisitos

- Node.js 18+
- NPM
- Git (opcional)
- Backend rodando em `http://localhost:8080`

---

## ▶️ Como executar

### Clonar o repositório

```bash
git clone https://github.com/edimichaellima/vue-agendamento.git
cd vue-agendamento
```

### Instalar dependências

```bash
npm install
```

### Rodar o frontend

```bash
npm run dev
```

Acesse:  
[http://localhost:5173](http://localhost:5173)

---

## 🌐 Integração com o Backend

- A API utilizada é servida via `http://localhost:8080/transferencias`
- O `axios` está configurado em `src/services/api.js`
- CORS deve estar habilitado no backend (`@CrossOrigin`)

---

## 📄 License

MIT (livre para uso acadêmico ou profissional).