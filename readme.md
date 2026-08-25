# ParkSim — Sistema Simulador de Estacionamento Inteligente

Projeto acadêmico da disciplina **Gestão e Qualidade de Software** — UNA Barreiro
**Professor:** Daniel Henrique Matos de Paiva

## 👥 Equipe

| Integrante | RA |
|---|---|
| João Vitor | 32513480 |
| Rafael Luiz Ferreira de Souza | 32511503 |
| Pietro Cardoso de Oliveira | 32515280 |

## 📌 Sobre o projeto

Aplicação web (HTML5 + CSS3 + JavaScript puro com ES Modules nativos, sem frameworks) que simula um estacionamento inteligente de 8 vagas. Veículos com placa Mercosul entram, estacionam e saem com animações fluidas, enquanto todo o ciclo de vida é persistido em tempo real no **Supabase (PostgreSQL em nuvem)** — com **TRIGGER** para cálculo do tempo de permanência, **RLS + Auth** para proteger o relatório e **exportação de PDF** com estatísticas da sessão.

## 🗂 Estrutura de arquivos e finalidade

```
projeto/
├── index.html      → estrutura da interface + CDNs (Supabase e jsPDF)
├── style.css       → tema dark, responsividade e animações
├── README.md       → este documento
└── js/
    ├── config.js      → constantes da simulação + credenciais Supabase
    ├── supabase.js    → criação do cliente Supabase (createClient)
    ├── banco.js       → camada de dados: INSERT/UPDATE/SELECT/DELETE, sessões e login
    ├── simulacao.js   → motor da simulação (requestAnimationFrame, spawn adaptativo)
    ├── ui.js          → DOM, animações dos carros (WAAPI), relatório e exportação de PDF
    └── app.js         → orquestrador: liga eventos, auth e limpeza do banco
```

| Arquivo | Funcionalidade |
|---|---|
| `index.html` | Controles da simulação (Iniciar/Pausar/Reiniciar, 1x/2x/3x), mapa do estacionamento (entrada, pista, 8 vagas, saída), painel administrativo (cards + tabela), modal de login e carregamento dos CDNs externos. |
| `style.css` | Tema escuro, layout responsivo (320px a 1440px+), animações da pista/carros e estilização de todos os componentes (cards, tabela, modal, painel travado). |
| `js/config.js` | Centraliza as constantes: total de vagas, intervalos de spawn, tempo de permanência, cores dos veículos e as chaves de acesso ao Supabase (URL + anon key). |
| `js/supabase.js` | Instancia e exporta o cliente Supabase usado pela camada de dados. |
| `js/banco.js` | Wrapper do Supabase: gerencia sessões (localStorage), autenticação (login/logout), registra entrada (INSERT), saída (UPDATE), consulta o relatório (SELECT com filtro por sessão) e limpa a tabela (DELETE) ao reiniciar/recarregar. |
| `js/simulacao.js` | Motor da simulação: loop com `requestAnimationFrame`, relógio simulado, velocidades 1x/2x/3x, spawn adaptativo de veículos e eventos de entrada/saída. |
| `js/ui.js` | Manipulação do DOM, animações dos carros via Web Animations API, atualização do relatório em tempo real e geração do relatório PDF (jsPDF + autotable) com estatísticas e conceitos de banco de dados. |
| `js/app.js` | Orquestrador central: conecta os eventos da simulação ao banco e à interface, aplica a autenticação (painel travado/liberado) e executa a limpeza do banco ao reiniciar o teste ou recarregar a página. |

## 🗄 Banco de dados (Supabase / PostgreSQL)

- **Tabela `movimentacoes`**: `id` (PK), `sessao`, `placa`, `cor`, `vaga`, `hora_entrada`, `hora_saida`, `tempo_minutos`, `status`;
- **TRIGGER `trg_calcular_tempo`**: calcula `tempo_minutos` automaticamente no UPDATE de saída;
- **RLS**: INSERT/UPDATE/DELETE liberados para a simulação; **SELECT restrito ao admin autenticado**;
- **Credenciais de teste**: `admin@parksim.com` / `admin123`.

## ▶️ Como executar localmente

1. Clone o repositório;
2. Abra a pasta com um servidor estático (Live Server no VS Code ou `npx serve`);
3. Acesse `http://127.0.0.1:5500`;
4. Faça login como admin para liberar o painel e exportar o PDF.

> O banco fica na nuvem (Supabase) — nenhum setup local é necessário.

## 📄 Arquivos de requisitos (Lista de Exercícios III)

| Arquivo | Finalidade |
|---|---|
| `documentacao.pdf` | Documento de Especificação Técnica: visão geral do sistema, matriz de requisitos (RF/RNF com critérios de aceite — ISO/IEC 25010), modelagem de dados (DER + SQL real), estratégia de versionamento e plano de testes (QA). |
| `apresentacao.pptx` | Apresentação executiva em 9 slides: capa, problema/escopo, RFs e fluxo crítico, RNFs, DER, módulos, pipeline Git, testes e conclusão. |

## 🔀 Versionamento e qualidade

- Repositório: `gqs-lista-03-analis-req` com **GitHub Flow** (branch `main` protegida + branches `feature/`, `fix/`, `docs/`);
- **Conventional Commits** (`feat`, `fix`, `docs`, `refactor`);
- **Pull Requests** com aprovação obrigatória de ao menos 1 integrante antes do merge.
