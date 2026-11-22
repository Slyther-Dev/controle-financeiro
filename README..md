# FinControl — Sistema de Controle Financeiro Pessoal

Aplicação web front-end para gestão financeira pessoal, desenvolvida com foco em **arquitetura limpa, responsividade e visualização de dados em tempo real**, sem dependência de servidores externos ou bancos de dados para uso imediato.

🔗 **Demo online:** [https://slyther-dev.github.io/controle-financeiro/](https://slyther-dev.github.io/controle-financeiro/)

---

## Visão Geral do Projeto

O **FinControl** permite registrar entradas e saídas, categorizar movimentações, acompanhar o saldo consolidado e analisar padrões de gastos por meio de gráficos dinâmicos. O projeto foi estruturado para demonstrar domínio dos fundamentos do desenvolvimento web moderno (HTML5 semântico, CSS utilitário e JavaScript modularizado em camada de estado, regras de negócio e renderização).

### Principais Funcionalidades

- **Dashboard com KPIs em Tempo Real:** cálculo automático de Receitas Totais, Despesas Totais e Saldo Atual.
- **Gestão de Transações (CRUD):** adição e exclusão de receitas e despesas com validação de campos obrigatórios e valores numéricos.
- **Categorização Inteligente:** classificação das movimentações (ex.: Salário, Freelance, Alimentação, Moradia, Transporte, Lazer, Saúde, Educação) para análise granular.
- **Visualização Gráfica Interativa:**
  - Gráfico de rosca (*Doughnut*) com a distribuição proporcional das despesas por categoria.
  - Gráfico de barras comparativo entre receitas e despesas.
- **Filtros e Busca:** filtragem rápida por tipo (Todas, Receitas, Despesas), categoria e pesquisa textual na descrição.
- **Persistência Local (`localStorage`):** armazenamento automático no navegador do usuário, mantendo os registros mesmo após recarregar ou fechar a página.
- **Feedback Visual (Toasts):** notificações não intrusivas para confirmar ações de cadastro, remoção ou erros de validação.

---

## Arquitetura e Decisões Técnicas

Embora a aplicação funcione em arquivo único (`index.html`) para facilitar o deploy estático e a portabilidade, o código JavaScript foi organizado seguindo o princípio de **separação de responsabilidades**:

1. **Gerenciamento de Estado (`State`):**
   - Centraliza a lista de transações em um array único de objetos padronizados (`id`, `description`, `amount`, `type`, `category`, `date`).
   - Garante que qualquer alteração dispare um ciclo previsível de atualização: `Mutação de Estado → Persistência no localStorage → Re-renderização da UI e Gráficos`.

2. **Camada de Persistência (`Storage`):**
   - Encapsula chamadas a `localStorage.getItem()` e `localStorage.setItem()` com tratamento de exceções (`try/catch`) e serialização JSON.
   - Inclui dados iniciais de demonstração (*seed data*) no primeiro acesso para evitar tela vazia (*empty state* frio) durante apresentações.

3. **Camada de Regras de Negócio e Agregação:**
   - Utiliza métodos funcionais de array (`filter`, `reduce`, `map`) para calcular totalizadores e agrupar gastos por categoria sem mutar o estado original.
   - Formatação monetária padronizada com a API nativa `Intl.NumberFormat('pt-BR', { style: 'currency', currency: 'BRL' })`.

4. **Camada de Visualização e DOM:**
   - Atualização reativa dos cards de resumo, tabela de histórico e instâncias do **Chart.js** (destruindo/atualizando gráficos corretamente para evitar sobreposição em canvas).

---

## Tecnologias Utilizadas

- **HTML5 Semântico:** estruturação acessível de formulários, tabelas e seções.
- **Tailwind CSS (via CDN):** estilização responsiva *mobile-first* com paleta consistente e hierarquia visual clara.
- **JavaScript (ES6+):** manipulação de DOM, `Intl.NumberFormat`, `localStorage`, eventos e funções puras de cálculo.
- **Chart.js:** renderização de gráficos responsivos e interativos em `<canvas>`.

---

## Como Executar Localmente

Nenhuma instalação de dependências (`npm install`) ou etapa de build é necessária:

1. Clone este repositório:
   ```bash
   git clone [https://github.com/Slyther-Dev/controle-financeiro.git](https://github.com/Slyther-Dev/controle-financeiro.git)