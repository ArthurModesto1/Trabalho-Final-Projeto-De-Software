# 🏋️ FitCore 💪

> Sistema de Gestão de Academia — controle completo de matrículas, treinos, agendamentos e pagamentos.

---

## 🚧 Status do Projeto

![Versão](https://img.shields.io/badge/Versão-v1.0.0-blue?style=for-the-badge)
![Node.js](https://img.shields.io/badge/Node.js-20.x-007ec6?style=for-the-badge&logo=nodedotjs&logoColor=white)
![React Native](https://img.shields.io/badge/React_Native-0.74-007ec6?style=for-the-badge&logo=react&logoColor=white)
![React](https://img.shields.io/badge/React-18.3-007ec6?style=for-the-badge&logo=react&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-5.4-007ec6?style=for-the-badge&logo=typescript&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-007ec6?style=for-the-badge&logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-7.2-007ec6?style=for-the-badge&logo=redis&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-25.0-007ec6?style=for-the-badge&logo=docker&logoColor=white)
![Licença](https://img.shields.io/badge/Licença-MIT-007ec6?style=for-the-badge&logo=opensourceinitiative)

---

## 📚 Índice

- [Links Úteis](#-links-úteis)
- [Sobre o Projeto](#-sobre-o-projeto)
- [Funcionalidades Principais](#-funcionalidades-principais)
- [Tecnologias Utilizadas](#-tecnologias-utilizadas)
- [Arquitetura](#-arquitetura)
- [Instalação e Execução](#-instalação-e-execução)
  - [Pré-requisitos](#pré-requisitos)
  - [Variáveis de Ambiente](#-variáveis-de-ambiente)
  - [Instalação de Dependências](#-instalação-de-dependências)
  - [Como Executar a Aplicação](#-como-executar-a-aplicação)
- [Deploy](#-deploy)
- [Estrutura de Pastas](#-estrutura-de-pastas)
- [Documentações Utilizadas](#-documentações-utilizadas)
- [Autores](#-autores)
- [Contribuição](#-contribuição)
- [Agradecimentos](#-agradecimentos)
- [Licença](#-licença)

---

## 🔗 Links Úteis

- 🌐 **Demo Online (Web Admin):** [https://fitcore-admin.vercel.app](https://fitcore-admin.vercel.app)
- 📱 **Download Mobile:** [App Store](#) | [Google Play](#) | [APK Direto](#)
- 📖 **Documentação da API:** [https://fitcore-api.vercel.app/api-docs](https://fitcore-api.vercel.app/api-docs)
- 🗂️ **Repositório:** [https://github.com/arthur-modesto/fitcore](https://github.com/ArthurModesto1/fitcore)

---

## 📝 Sobre o Projeto

O **FitCore** é um sistema de gestão de academia desenvolvido como projeto acadêmico da disciplina **Projeto de Software** do curso de Engenharia de Software da PUC Minas.

O sistema nasce da necessidade real de academias de médio porte que ainda gerenciam matrículas em planilhas, controlam check-ins manualmente e não possuem integração entre pagamentos e acesso físico. O FitCore resolve esse problema oferecendo uma plataforma centralizada com:

- **App Mobile** para alunos realizarem check-in, agendarem aulas e acompanharem treinos.
- **Web App** para administradores e funcionários gerenciarem toda a operação.
- **Backend em microsserviços** escalável, hospedado na AWS com alta disponibilidade.

O projeto entrega valor imediato ao gestor da academia (redução de inadimplência, controle de acesso automatizado) e ao aluno (autonomia para contratar planos, agendar aulas e pagar mensalidades pelo celular).

---

## ✨ Funcionalidades Principais

- 🔐 **Autenticação Segura:** Login via JWT, cadastro de alunos com validação de CPF e recuperação de senha por e-mail.
- 🏷️ **Gestão de Planos e Matrículas:** Criação, contratação e renovação de planos com controle de vencimento automático.
- 💳 **Pagamentos Online:** Processamento de mensalidades via Stripe com suporte a cartão de crédito, débito e Pix.
- 📲 **Check-in Digital:** Alunos realizam check-in pelo app via QR Code; funcionários registram presença pelo sistema web.
- 🗓️ **Agendamento de Aulas Coletivas:** Reserva de vagas em aulas com controle de lotação em tempo real via Redis.
- 🏃 **Fichas de Treino:** Funcionários cadastram rotinas de treino personalizadas por aluno.
- 📊 **Relatórios Gerenciais:** Dashboard com frequência, inadimplência, ocupação de aulas e receita mensal.
- 🔔 **Notificações Push:** Alertas de vencimento de plano, confirmação de agendamento e lembretes de aula via Firebase FCM.

---

## 🛠 Tecnologias Utilizadas

### 📱 Mobile

- **Framework:** React Native 0.74
- **Linguagem:** TypeScript 5.4
- **Navegação:** React Navigation 6
- **HTTP Client:** Axios
- **Notificações:** Firebase Cloud Messaging (FCM)
- **Build:** Expo (EAS Build)

### 💻 Front-end Web

- **Framework:** React 18.3
- **Linguagem:** TypeScript 5.4
- **Build Tool:** Vite 5.2
- **Estilização:** Tailwind CSS 3.4
- **Gerenciamento de Estado:** Zustand 4.5
- **Gráficos:** Recharts 2.12

### 🖥️ Back-end (Microsserviços)

- **Runtime:** Node.js 20 LTS
- **Framework:** Express 4.19 (por serviço)
- **Linguagem:** TypeScript 5.4
- **ORM:** Prisma 5.14
- **Autenticação:** JWT + Bcrypt
- **Banco de Dados:** PostgreSQL 15
- **Cache:** Redis 7.2
- **Pagamentos:** Stripe API v14
- **Notificações:** Firebase Admin SDK

### ⚙️ Infraestrutura & DevOps

- **Containerização:** Docker 25 + Docker Compose
- **Orquestração:** AWS ECS (Elastic Container Service)
- **Banco Gerenciado:** AWS RDS (PostgreSQL 15)
- **Cache Gerenciado:** AWS ElastiCache (Redis 7)
- **CDN/Frontend:** AWS CloudFront + S3
- **CI/CD:** GitHub Actions
- **Monitoramento:** AWS CloudWatch

---

## 🏗 Arquitetura

O FitCore adota uma **arquitetura de microsserviços** com separação clara entre frontend, API Gateway e serviços de domínio. Cada serviço é responsável por um contexto delimitado (bounded context) do negócio, comunicando-se exclusivamente via API Gateway.

**Serviços de domínio:**
- **Matrículas** (porta 3001): Gestão de planos, contratos e renovações.
- **Treinos** (porta 3002): Fichas e exercícios personalizados.
- **Agendamentos** (porta 3003): Reservas de aulas coletivas com controle de vagas via Redis.
- **Financeiro** (porta 3004): Faturas, pagamentos e integração com Stripe.

**Padrões adotados:** Repository Pattern, Service Layer, DTO, Adapter (StripeAdapter), e Single Table Inheritance para hierarquia de usuários.

### Diagramas

Os diagramas completos do sistema estão na pasta `/diagramas` do repositório, organizados por tipo:

| Tipo | Localização |
|---|---|
| Arquitetura (C4) | `diagramas/arquitetura/arq_fitcore.puml` |
| Casos de Uso | `diagramas/casos-de-uso/uc_fitcore.puml` |
| Classes | `diagramas/classes/class_fitcore.puml` |
| Componentes | `diagramas/componentes-implantacao/comp_fitcore.puml` |
| Implantação | `diagramas/componentes-implantacao/impl_fitcore.puml` |
| Sequência de Sistema | `diagramas/sequencia-sistema/` |
| Sequência de Projeto | `diagramas/sequencia/` |
| Comunicação | `diagramas/comunicacao/` |
| Estados | `diagramas/estados/` |
| Entidade-Relacionamento | `diagramas/dados/er_fitcore.puml` |

---

## 🔧 Instalação e Execução

### Pré-requisitos

- **Node.js:** v20 LTS ou superior
- **npm:** v10 ou superior
- **Docker** e **Docker Compose** (recomendado para banco e cache)
- **Git**

---

### 🔑 Variáveis de Ambiente

Crie um arquivo **`.env`** na raiz de cada serviço de backend com base nos exemplos abaixo.

#### Back-end (cada microsserviço)

| Variável | Descrição | Exemplo |
|---|---|---|
| `PORT` | Porta do serviço | `3001` |
| `DATABASE_URL` | URL de conexão PostgreSQL (Prisma) | `postgresql://postgres:senha@localhost:5432/fitcore` |
| `REDIS_URL` | URL de conexão Redis | `redis://localhost:6379` |
| `JWT_SECRET` | Chave secreta para tokens JWT | `chave_super_segura_256bits` |
| `STRIPE_SECRET_KEY` | Chave secreta da API Stripe | `sk_test_...` |
| `FIREBASE_PROJECT_ID` | ID do projeto Firebase | `fitcore-app` |
| `FIREBASE_PRIVATE_KEY` | Chave privada do Firebase Admin | `-----BEGIN RSA PRIVATE KEY-----...` |

#### Front-end Web (`.env` na pasta `/web`)

| Variável | Descrição | Exemplo |
|---|---|---|
| `VITE_API_URL` | URL base do API Gateway | `http://localhost:4000/api` |
| `VITE_STRIPE_PUBLIC_KEY` | Chave pública do Stripe | `pk_test_...` |

---

### 📦 Instalação de Dependências

**1. Clone o repositório:**
```bash
git clone https://github.com/arthur-modesto/fitcore.git
cd fitcore
```

**2. Instale as dependências do Front-end Web:**
```bash
cd web
npm install
cd ..
```

**3. Instale as dependências de cada microsserviço:**
```bash
cd services/matriculas && npm install && cd ../..
cd services/treinos && npm install && cd ../..
cd services/agendamentos && npm install && cd ../..
cd services/financeiro && npm install && cd ../..
cd gateway && npm install && cd ..
```

---

### ⚡ Como Executar a Aplicação

#### 🐳 Execução completa com Docker Compose (recomendado)

Sobe todos os serviços (PostgreSQL, Redis, Gateway e microsserviços) de uma vez:

```bash
docker-compose up --build -d
```

Verifique se os containers estão rodando:
```bash
docker ps
```

Execute as migrações do banco (na primeira execução):
```bash
docker exec fitcore-matriculas npx prisma migrate deploy
docker exec fitcore-financeiro npx prisma migrate deploy
docker exec fitcore-agendamentos npx prisma migrate deploy
docker exec fitcore-treinos npx prisma migrate deploy
```

#### Terminal 1 — Front-end Web

```bash
cd web
npm run dev
```
🎨 Disponível em **http://localhost:5173**

#### Terminal 2 — API Gateway

```bash
cd gateway
npm run dev
```
🚀 Disponível em **http://localhost:4000**

#### Terminais 3–6 — Microsserviços

```bash
# Em terminais separados:
cd services/matriculas && npm run dev    # :3001
cd services/treinos && npm run dev       # :3002
cd services/agendamentos && npm run dev  # :3003
cd services/financeiro && npm run dev    # :3004
```

Para parar todos os containers:
```bash
docker-compose down
```

---

## 🚀 Deploy

**1. Build dos artefatos:**
```bash
# Front-end Web
cd web && npm run build

# Microsserviços (Docker image)
docker build -t fitcore-matriculas ./services/matriculas
docker build -t fitcore-treinos ./services/treinos
docker build -t fitcore-agendamentos ./services/agendamentos
docker build -t fitcore-financeiro ./services/financeiro
```

**2. Push para o ECR (AWS Elastic Container Registry):**
```bash
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <account_id>.dkr.ecr.us-east-1.amazonaws.com
docker tag fitcore-matriculas <account_id>.dkr.ecr.us-east-1.amazonaws.com/fitcore-matriculas:latest
docker push <account_id>.dkr.ecr.us-east-1.amazonaws.com/fitcore-matriculas:latest
```

**3. Deploy do Front-end no S3 + CloudFront:**
```bash
aws s3 sync web/dist s3://fitcore-web-bucket --delete
aws cloudfront create-invalidation --distribution-id <ID> --paths "/*"
```

> O CI/CD via **GitHub Actions** automatiza todo esse processo a cada push na branch `main`.

---

## 📂 Estrutura de Pastas

```
fitcore/
│
├── .github/
│   └── workflows/
│       └── deploy.yml           # CI/CD com GitHub Actions
│
├── diagramas/                   # Todos os diagramas PlantUML do projeto
│   ├── arquitetura/
│   ├── casos-de-uso/
│   ├── classes/
│   ├── componentes-implantacao/
│   ├── comunicacao/
│   ├── dados/
│   ├── estados/
│   ├── sequencia/
│   └── sequencia-sistema/
│
├── docs/                        # Documentação de projeto (.docx, .pdf)
│
├── gateway/                     # API Gateway (Node.js / Express)
│   ├── src/
│   │   ├── middlewares/         # Auth, RateLimit, Logger
│   │   └── routes/              # Roteamento para microsserviços
│   ├── .env.example
│   ├── Dockerfile
│   └── package.json
│
├── services/
│   ├── matriculas/              # Serviço de Matrículas (:3001)
│   │   ├── src/
│   │   │   ├── controllers/     # MatriculaCtrl, PlanoCtrl
│   │   │   ├── services/        # MatriculaSvc, PlanoSvc, NotifSvc
│   │   │   ├── repositories/    # MatriculaRepo, PlanoRepo
│   │   │   └── domain/          # Entidades e enums de domínio
│   │   ├── prisma/
│   │   │   └── schema.prisma
│   │   ├── .env.example
│   │   ├── Dockerfile
│   │   └── package.json
│   │
│   ├── treinos/                 # Serviço de Treinos (:3002)
│   ├── agendamentos/            # Serviço de Agendamentos (:3003)
│   └── financeiro/              # Serviço Financeiro (:3004)
│
├── web/                         # Front-end Web Admin (React + Vite)
│   ├── src/
│   │   ├── components/          # Componentes reutilizáveis
│   │   ├── pages/               # Páginas por módulo
│   │   ├── services/            # Chamadas HTTP (Axios)
│   │   ├── hooks/               # Hooks customizados
│   │   ├── store/               # Estado global (Zustand)
│   │   └── styles/              # Tailwind config, tema global
│   ├── .env.example
│   ├── Dockerfile
│   └── package.json
│
├── mobile/                      # App Mobile (React Native / Expo)
│   ├── src/
│   │   ├── screens/             # Telas do app
│   │   ├── navigation/          # React Navigation
│   │   ├── services/            # API calls
│   │   └── components/          # UI components
│   └── package.json
│
├── docker-compose.yml           # Orquestração local completa
├── docker-compose.override.yml  # Overrides de desenvolvimento
├── README.md
└── LICENSE
```

---

## 🔗 Documentações Utilizadas

- 📖 **PlantUML:** [https://plantuml.com](https://plantuml.com)
- 📖 **C4 Model (C4-PlantUML):** [https://github.com/plantuml-stdlib/C4-PlantUML](https://github.com/plantuml-stdlib/C4-PlantUML)
- 📖 **Prisma ORM:** [https://www.prisma.io/docs](https://www.prisma.io/docs)
- 📖 **React Native:** [https://reactnative.dev/docs/getting-started](https://reactnative.dev/docs/getting-started)
- 📖 **Express.js:** [https://expressjs.com](https://expressjs.com)
- 📖 **Stripe API:** [https://stripe.com/docs/api](https://stripe.com/docs/api)
- 📖 **Firebase Admin SDK:** [https://firebase.google.com/docs/admin/setup](https://firebase.google.com/docs/admin/setup)
- 📖 **Docker Compose:** [https://docs.docker.com/compose](https://docs.docker.com/compose)
- 📖 **AWS ECS:** [https://docs.aws.amazon.com/ecs](https://docs.aws.amazon.com/ecs)
- 📖 **Redis:** [https://redis.io/docs](https://redis.io/docs)
- 📖 **Conventional Commits:** [https://www.conventionalcommits.org](https://www.conventionalcommits.org/en/v1.0.0/)

---

## 👥 Autores

| 👤 Nome | 🐙 GitHub | 💼 LinkedIn |
|---|---|---|
| Arthur Modesto Couto | [@ArthurModesto1](https://github.com/ArthurModesto1) | [linkedin.com/in/arthur-modesto](https://linkedin.com/in/arthurmodeto) |

---

## 🤝 Contribuição

1. Faça um `fork` do projeto.
2. Crie uma branch para sua feature:
   ```bash
   git checkout -b feature/minha-feature
   ```
3. Commit suas mudanças seguindo Conventional Commits:
   ```bash
   git commit -m 'feat: adiciona agendamento recorrente de aulas'
   ```
4. Faça o push para a branch:
   ```bash
   git push origin feature/minha-feature
   ```
5. Abra um **Pull Request**.

---

## 🙏 Agradecimentos

- [**Engenharia de Software PUC Minas**](https://www.instagram.com/engsoftwarepucminas/) — Pelo suporte institucional e fomento às boas práticas de engenharia.
- [**Prof. Dr. João Paulo Aramuni**](https://github.com/joaopauloaramuni) — Pelos ensinamentos em Arquitetura de Software, Padrões de Projeto e pela orientação durante toda a disciplina.

---

## 📄 Licença

Este projeto é distribuído sob a **Licença MIT**.
Consulte o arquivo [LICENSE](./LICENSE) para mais detalhes.
