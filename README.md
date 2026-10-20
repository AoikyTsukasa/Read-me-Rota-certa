RotaCerta AI — Plataforma Inteligente de Logística e Entregas
**Componente Curricular:** Engenharia de Software I (IES-013)
**Curso:** Tecnologia em Big Data para a Indústria — Fatec São Carlos
**Guilda:** Rota 66 (Grupo 04)
---
Integrantes e Papéis na Equipe
O trabalho em nossa guilda utiliza um sistema de rodízio de papéis a cada duas aulas [1, 2]:
| Integrante | Usuário GitHub | Papel Inicial | Responsabilidade Principal |
| :--- | :--- | :--- | :--- |
| **Ana Souza** | \`@anasouza\` | **Product Owner** | Gestão do backlog e interface com o cliente [1, 2] |
| **Bruno Lima** | \`@brunolima\` | **Escriba** | Manutenção do \`README.md\`, diagramas e ADRs [1, 2] |
| **Carla Mendes**| \`@carlamendes\`| **Integrador** | Administração de repositório, branches e releases [1, 2] |
| **Diego Alves** | \`@diegoalves\` | **Qualidade** | Casos de teste, revisão de PRs e garantia de cobertura [1, 2] |
---
Descricao
O **RotaCerta AI** é uma plataforma web e mobile voltada para a gestão e otimização de entregas urbanas de curto alcance. O sistema conecta estabelecimentos comerciais, entregadores autônomos e clientes finais.

Diferente de scripts isolados que rodam apenas na máquina do desenvolvedor [3, 4], o **RotaCerta AI** foi projetado como um software completo [3, 4]: possui versionamento transparente, suíte automatizada de testes, documentação viva e infraestrutura reproduzível [3, 5].

Especificação do Agente Inteligente (PEAS) O núcleo do sistema conta com um agente racional de otimização de rotas [6, 7], cuja especificação **PEAS** [8, 9] é detalhada a seguir:

**P (Medida de Desempenho / Performance):** Minimização do tempo total de entrega, redução do consumo de combustível (km rodados) e taxa de pontualidade de entregas [8, 9].

**E (Ambiente / Environment):** Malha viária urbana, condições de tráfego em tempo real, disponibilidade de entregadores e janelas de horário dos clientes [8, 9].

**A (Atuadores / Actuators):** Atribuição de pedidos a entregadores, envio de rota otimizada para o app mobile e notificações de status [8, 9].

**S (Sensores / Sensors):** GPS dos dispositivos móveis, API de tráfego viário, confirmações de retirada/entrega via app [8, 9].
---
Tecnologias, Ferramentas e Infraestrutura

**Front-end &amp; Mobile**

**React Native (Expo):** Aplicação mobile para entregadores e clientes.

**React.js / TailwindCSS:** Painel web administrativo para estabelecimentos comerciais.

**Back-end &amp; Algoritmos**

**Python 3.12 (FastAPI):*** API de alta performance para gerenciamento de pedidos e microsserviços.

**Módulo de Busca em Python:** Algoritmo de busca heurística \\\\(A^\*\\\\) em grafo com filas de prioridade e dicionários nativos (\`mapa\_romenia\` / grafos viários) [10-12].

**Banco de Dados &amp; Infraestrutura**

**PostgreSQL / PostGIS:** Banco de dados relacional com suporte a dados geoespaciais.

**Redis:** Cache de sessões e fila de mensagens em tempo real.

**Docker &amp; Docker Compose:** Conteinerização de todos os serviços para garantir reprodutibilidade do ambiente [13].
---
Metodologia de Desenvolvimento e Processo

**Modelo de Processo Escolhido: Espiral com Entregas Incrementais**

Para este projeto, descartamos o modelo **Cascata** [14, 15]. Em sistemas orientados a dados e mobilidade, os requisitos dependem da exploração direta do comportamento viário [13, 16]. No Cascata, os testes e validações ocorrem apenas ao final do ciclo, fazendo com que a descoberta de erros na produção custe até **100x mais** do que na fase de especificação [5, 15, 17].

Optamos pela abordagem **Espiral** combinada com entregas **Incrementais** [16, 18]: 1. **Fatiamento por Risco (Espiral):** Cada volta da espiral resolve uma incerteza crítica [16, 18] — como validar a qualidade dos dados viários e a latência da API de rotas através de um protótipo descartável [16, 19]. 2. **Fatiamento por Valor (Incremental):** Cada incremento entrega um módulo funcional ao cliente (Ex.: Sprint 1: Cadastro de Pedidos; Sprint 2: Roteamento Estático; Sprint 3: Roteamento em Tempo Real) [16, 18].

**Decisão Arquitetural Registrada (ADR):** &gt; A justificativa detalhada, juntamente com as alternativas descartadas e consequências, encontra-se documentada no arquivo [`docs/decisoes/001-processo.md`](docs/decisoes/001-processo.md) [20, 21].
---
Gestão de Configuração e Uso do Git

Seguimos as boas práticas de Engenharia de Software para manter o repositório limpo e auditável [5, 22]:

**Estrutura de Branches:**

* `main\`: Código estável e pronto para produção (apenas recebe código via *Pull Request*) [23, 24].

* `feature/*`: Ramos temporários para desenvolvimento de funcionalidades específicas.

* `docs/*`: Ramos para atualizações da documentação da guilda.

**Politica de Pull Requests e Revisão por Pares:**

* Nenhuma alteração entra na `main` sem a aprovação do responsável pela **Qualidade** da guilda ou revisão de outra guilda [1, 25, 26].

* Commits devem possuir mensagens curtas e descritivas (Ex: 'feat: adiciona algoritmo A* para busca de rotas` ou `docs: atualiza ADR 001`) [24, 27, 28].

**Arquivo `.gitignore`:** Mantemos o repositório livre de arquivos temporários do ambiente local [22]:
```gitignore
# PyCharm e configurações de IDE .idea/
# Arquivos compilados do Python _\_pycache_/ *.pyc
# Ambiente virtual .venv/ venv/

+--------------------------------------------------+
| [<=] RotaCerta AI [ Notificações ] |
+--------------------------------------------------+
| Acompanhe sua Entrega (#1042)                    |
|                                                  |
| +--------------------------------------------+   |
| |               MAPA INTERATIVO                | |
| |   [Restaurante] --------&gt; 🏍️ (Entregador)| |
| |                                \             | |
| |                                 -----&gt; 🏠 | |
|   +--------------------------------------------+  |
|                                                  |
| Status: Entregador a caminho (Estimativa: 8 min) |
| Entregador: Carlos Silva (Honda CG 160)          |
|                                                  |
|     [ Cancelar Pedido ] [ Contatar Suporte ]     |
+--------------------------------------------------+
