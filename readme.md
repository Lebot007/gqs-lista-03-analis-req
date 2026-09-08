<div align="center">

# 🅿️ ParkSim
### Sistema Simulador de Estacionamento Inteligente

Projeto acadêmico da disciplina **Gestão e Qualidade de Software** — UNA Barreiro
**Professor:** Daniel Henrique Matos de Paiva

[![Python](https://img.shields.io/badge/Python-3.12-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-API-009688?style=flat-square&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![Supabase](https://img.shields.io/badge/Supabase-PostgreSQL-3ECF8E?style=flat-square&logo=supabase&logoColor=white)](https://supabase.com/)
[![JavaScript](https://img.shields.io/badge/JavaScript-ES%20Modules-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](https://developer.mozilla.org/docs/Web/JavaScript)
[![Tests](https://img.shields.io/badge/tests-28%20passed-2ECC71?style=flat-square&logo=pytest&logoColor=white)](#-testes-automatizados)
[![License](https://img.shields.io/badge/license-academic-lightgrey?style=flat-square)](#)

</div>

<br>

## 📑 Sumário

- [Sobre o projeto](#-sobre-o-projeto)
- [Arquitetura](#️-arquitetura)
- [Tecnologias utilizadas](#-tecnologias-utilizadas)
- [Estrutura do projeto](#-estrutura-do-projeto)
- [Responsabilidades dos arquivos](#-responsabilidades-dos-arquivos)
- [Funcionalidades principais](#-funcionalidades-principais)
- [API disponível](#-api-disponível)
- [Banco de dados](#-banco-de-dados)
- [Como executar](#️-como-executar)
- [Testes automatizados](#-testes-automatizados)
- [Qualidade de software](#-qualidade-de-software)
- [Integração contínua](#-integração-contínua)
- [Documentação complementar](#-documentação-complementar)
- [Status do projeto](#-status-do-projeto)
- [Equipe](#-equipe)

<br>

## 👥 Equipe

| Integrante | RA |
|---|---|
| João Vitor | 32513480 |
| Rafael Luiz Ferreira de Souza | 32511503 |
| Pietro Cardoso de Oliveira | 32515280 |

<br>

## 📖 Sobre o projeto

O **ParkSim** é uma aplicação web que simula o fluxo de veículos em um estacionamento inteligente com **8 vagas**.

O sistema representa:

- 🚗 entrada de veículos
- 🅿️ escolha de vaga
- ⏱️ permanência
- 🚪 saída
- 📊 ocupação das vagas
- 🗂️ registro das movimentações
- 🔐 painel administrativo
- 📈 estatísticas da sessão
- 📄 exportação de relatório em PDF

O projeto busca resolver um problema real: **a falta de visibilidade sobre o fluxo de entrada, ocupação e saída de veículos em estacionamentos.**

> 🌍 A solução está relacionada à **ODS 11 — Cidades e Comunidades Sustentáveis**, por abordar organização, monitoramento e gestão de espaços urbanos.

<br>

## 🏗️ Arquitetura

O projeto utiliza uma arquitetura em três camadas:

```text
Frontend JavaScript
        ↓
API Python/FastAPI
        ↓
Supabase/PostgreSQL
```

> ⚠️ O frontend **não** acessa diretamente o Supabase. Todas as operações de dados passam pelo backend Python.

<br>

## 🧰 Tecnologias utilizadas

<table>
<tr>
<td valign="top" width="33%">

**Frontend**
- HTML5
- CSS3
- JavaScript ES Modules
- Web Animations API
- `requestAnimationFrame`
- jsPDF
- jsPDF AutoTable
- Live Server

</td>
<td valign="top" width="33%">

**Backend**
- Python 3.12
- FastAPI
- Uvicorn
- Pydantic
- python-dotenv
- Supabase Python Client
- pytest
- HTTPX

</td>
<td valign="top" width="33%">

**Banco de dados**
- PostgreSQL
- Supabase
- Tabela `movimentacoes`
- Trigger para cálculo do tempo de permanência
- Autenticação administrativa

</td>
</tr>
</table>

<br>

## 📁 Estrutura do projeto

<details>
<summary><strong>Clique para expandir a árvore de diretórios</strong></summary>

```text
projeto/
├── .github/
│   └── workflows/
│       └── ci.yml
│
├── backend/
│   ├── .env.example
│   ├── requirements.txt
│   │
│   ├── app/
│   │   ├── __init__.py
│   │   ├── config.py
│   │   ├── main.py
│   │   ├── regras.py
│   │   ├── repositorio.py
│   │   └── schemas.py
│   │
│   └── tests/
│       ├── __init__.py
│       ├── test_api.py
│       └── test_regras.py
│
├── js/
│   ├── app.js
│   ├── banco.js
│   ├── config.js
│   ├── simulacao.js
│   └── ui.js
│
├── index.html
├── style.css
├── README.md
├── estrutura.txt
├── especificacao_tecnica_parksim_revisada.pdf
└── ParkSim_Apresentacao_revisada.pptx
```

</details>

<br>

## 🧩 Responsabilidades dos arquivos

**Frontend**

| Arquivo | Responsabilidade |
|---|---|
| `index.html` | Estrutura da interface |
| `style.css` | Tema visual, responsividade e animações |
| `js/app.js` | Orquestração dos eventos, autenticação e simulação |
| `js/banco.js` | Comunicação com a API Python usando `fetch` |
| `js/config.js` | Constantes da simulação e URL da API |
| `js/simulacao.js` | Motor da simulação, vagas, placas, entradas e saídas |
| `js/ui.js` | Atualização do DOM, tabela, métricas, animações e exportação PDF |

**Backend**

| Arquivo | Responsabilidade |
|---|---|
| `backend/app/main.py` | Aplicação FastAPI, endpoints e tratamento de erros |
| `backend/app/regras.py` | Regras de negócio e validações |
| `backend/app/repositorio.py` | Conexão e operações no Supabase/PostgreSQL |
| `backend/app/schemas.py` | Modelos de entrada usando Pydantic |
| `backend/app/config.py` | Leitura das variáveis de ambiente |
| `backend/tests/` | Testes unitários e testes da API |

<br>

## ⚙️ Funcionalidades principais

- ✅ Simulação de estacionamento com 8 vagas
- ✅ Geração de placas no padrão Mercosul
- ✅ Escolha aleatória de cores
- ✅ Entrada e saída de veículos
- ✅ Controles de iniciar, pausar e reiniciar
- ✅ Velocidades de simulação 1x, 2x e 3x
- ✅ Registro persistente das movimentações
- ✅ Login administrativo
- ✅ Painel protegido para consulta do relatório
- ✅ Métricas de veículos, estacionados, saídas e tempo médio
- ✅ Tabela com as movimentações recentes
- ✅ Exportação do relatório em PDF
- ✅ Tratamento de erros de conexão, validação e autenticação

<br>

## 🔌 API disponível

| Método | Rota | Finalidade |
|---|---|---|
| `GET` | `/health` | Verificar se a API está funcionando |
| `POST` | `/auth/login` | Realizar login administrativo |
| `GET` | `/movimentacoes` | Consultar movimentações |
| `GET` | `/relatorio/resumo` | Consultar resumo da sessão |
| `POST` | `/movimentacoes` | Registrar entrada |
| `PATCH` | `/movimentacoes/saida` | Registrar saída |
| `DELETE` | `/movimentacoes` | Limpar movimentações |

<br>

## 🗄️ Banco de dados

A tabela principal utilizada pelo sistema é `movimentacoes`.

**Campos principais:**

`id` · `sessao` · `placa` · `cor` · `vaga` · `hora_entrada` · `hora_saida` · `tempo_minutos` · `status`

O Supabase utiliza PostgreSQL em nuvem. O backend Python acessa o banco por meio da biblioteca `supabase`.

A saída de um veículo atualiza `hora_saida` e `status`. O cálculo de `tempo_minutos` é realizado pela regra configurada no banco por meio de trigger.

> 🔒 As credenciais secretas devem permanecer somente no arquivo local `backend/.env`. Esse arquivo **não** deve ser enviado ao GitHub.

<br>

## ▶️ Como executar

### 1. Criar o ambiente virtual

No Windows:

```powershell
cd backend
python -m venv .venv
.venv\Scripts\activate
```

### 2. Instalar as dependências

```powershell
pip install -r requirements.txt
```

### 3. Configurar o ambiente

Crie o arquivo `backend/.env`:

```env
SUPABASE_URL=https://seu-projeto.supabase.co
SUPABASE_SERVICE_KEY=sua_chave_secreta
```

> ⚠️ Nunca publique a chave secreta no GitHub ou no frontend.

### 4. Executar os testes

```powershell
python -m pytest -v
```

Resultado atual da suíte:

```text
28 passed
```

### 5. Iniciar a API

```powershell
uvicorn app.main:app --reload --port 8000
```

A API ficará disponível em:

```text
http://127.0.0.1:8000
```

Para verificar:

```text
http://127.0.0.1:8000/health
```

A resposta esperada é:

```json
{
  "status": "ok"
}
```

### 6. Iniciar o frontend

Mantenha a API rodando e abra o `index.html` usando o **Live Server** do VS Code.

O frontend normalmente ficará disponível em:

```text
http://127.0.0.1:5500
```

> ℹ️ A API Python e o Live Server precisam estar rodando simultaneamente.

<br>

## 🧪 Testes automatizados

Os testes cobrem:

- validação de placas
- validação de cores
- validação de vagas
- cálculo de permanência
- tempo mínimo de permanência
- média de tempos
- frequência de cores e vagas
- criação de movimentações
- rejeição de dados inválidos
- registro de saída
- retorno 404 para veículo inexistente
- autenticação sem token
- limpeza de registros

> 🧵 Os testes da API utilizam um repositório falso (`RepoFalso`) para evitar dependência de rede ou do banco real durante a execução da suíte.

<br>

## ✅ Qualidade de software

O projeto aplica:

- separação de responsabilidades
- regras de negócio isoladas
- tratamento de erros com `try/except`
- respostas HTTP adequadas
- modelos Pydantic
- testes automatizados
- documentação técnica
- integração contínua configurada
- arquitetura em camadas
- uso de variáveis de ambiente
- proteção das credenciais secretas

<br>

## 🔄 Integração contínua

O arquivo `.github/workflows/ci.yml` configura um workflow para:

1. utilizar Python 3.12;
2. instalar as dependências;
3. executar os testes com pytest.

**Estratégia de versionamento planejada:**

| Branch | Finalidade |
|---|---|
| `main` | Versão estável |
| `develop` | Integração |
| `feature/*` | Novas funcionalidades |
| `fix/*` | Correções |
| `docs/*` | Documentação |

Também são recomendados **commits semânticos**, como:

```text
feat: adiciona API FastAPI
fix: corrige registro de saída
test: adiciona testes de validação
docs: atualiza documentação
ci: configura workflow de testes
```

<br>

## 📚 Documentação complementar

Este projeto possui:

- 📄 documento de especificação técnica
- 📊 apresentação PowerPoint
- 📋 matriz de requisitos
- 🧪 plano de testes
- 🏗️ documentação da arquitetura
- ⚙️ testes automatizados
- 🔄 workflow de integração contínua

<br>

## 📌 Status do projeto

O projeto possui:

- [x] frontend funcional
- [x] backend Python/FastAPI funcional
- [x] integração com Supabase/PostgreSQL
- [x] autenticação administrativa
- [x] testes automatizados
- [x] relatório em PDF
- [x] documentação técnica
- [x] CI configurado

> 🚧 A publicação do repositório, branches, Pull Requests e execução do workflow na nuvem dependem da etapa de upload para o GitHub.

<br>

<div align="center">

**Gestão e Qualidade de Software** · UNA Barreiro · 2026

</div>
