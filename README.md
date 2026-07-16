# 📊 Dashboard de Vendas 
Entrega da Semana 8 - Capacitação de Ciência de Dados

## 1. Objetivo

Este arquivo (`Dashboard_-_Semana_8.xlsm`) é um dashboard interativo construído a partir de uma base de dados de vendas, aplicando os conceitos trabalhados na capacitação: tratamento e padronização de base, manipulação de texto, criação de indicadores, tabelas dinâmicas, gráficos analíticos, estruturação de dashboard executivo e automação básica com macros.

O arquivo é `.xlsm` (habilitado para macro) — ao abrir, é necessário **habilitar macros/conteúdo ativo** para que os botões de navegação funcionem.

---

## 2. Estrutura do arquivo (abas)

| Aba | Visibilidade | Função |
|---|---|---|
| `Base de Dados` | Oculta | Base bruta original, importada sem alterações. Mantida como registro/backup. |
| `Tabelas Auxiliares` | Oculta | Tabelas de apoio usadas nos `VLOOKUP` (ex: hierarquia vendedor → supervisor → gerente → equipe; marca; categoria). |
| `Base de Dados (Tratada)` | Visível | Base tratada e enriquecida — é a fonte real de todas as tabelas dinâmicas e gráficos. |
| `Tabelas Dinâmicas` | Visível | As 9 tabelas dinâmicas que alimentam o dashboard (faturamento por mês, por vendedor, por categoria, por ano, KPIs). |
| `Aux_Mensal48` | Oculta | Série mensal real (4 anos × 12 meses = 48 pontos), usada para o cálculo correto de volatilidade/estabilidade na aba de Perguntas e Respostas. |
| `Layout` | Visível | Rascunho/estrutura visual de apoio para a montagem do dashboard. |
| `DashBoard` | Visível | **Aba principal** — KPIs, gráficos e slicers, para visualização executiva. |
| `Perguntas e Respostas` | Visível | Respostas às perguntas de negócio levantadas a partir dos dados. |

> Abas ocultas guardam a base bruta e cálculos auxiliares — foram ocultadas para não poluir a navegação, mas continuam ativas e recalculando normalmente.

---

## 3. Tratamento e padronização da base

Na aba `Base de Dados (Tratada)`, a tabela `Tabela2` (A6:W33551) aplica, por fórmula (nunca valor fixo):

- **Extração de data**: `Ano` (`=YEAR(...)`) e `Mês` (`=MONTH(...)`) a partir de `Data_Venda`.
- **Nome do mês por extenso**: gerado via `=PRI.MAIÚSCULA(TEXTO(DATA([@Ano];[@Mês];1);"mmmm"))`.
- **Enriquecimento via `VLOOKUP`**: Supervisor, Gerente e Equipe de Vendas (a partir do vendedor), Marca (a partir do produto) e Categoria (a partir da subcategoria), todos puxados de `Tabelas Auxiliares`.
- **Indicadores por linha**: `Valor Desconto` (Preço Unitário × Desconto) e `Valor Total` (Quantidade × (Preço Unitário − Valor Desconto)).

---

## 4. Indicadores (KPIs) do dashboard

Calculados a partir das tabelas dinâmicas e exibidos como cartões na aba `DashBoard`:

- **Faturamento Total**: R$ 1.221.063.833,19
- **Ticket Médio**: R$ 36.400,77
- **Média de Desconto**: 8,01%
- **Quantidade de Vendas**: 436.570

---

## 5. Tabelas dinâmicas e gráficos

9 tabelas dinâmicas na aba `Tabelas Dinâmicas` alimentam 4 gráficos no `DashBoard`:

- Faturamento por mês (linha)
- Faturamento por vendedor (barras)
- Faturamento por categoria (barras)
- Volume de vendas por ano (barras)

Há **slicers** conectados às tabelas dinâmicas para filtrar o dashboard interativamente.

---

## 6. Automação com macros

Módulo VBA (`Módulo1`) com rotinas de navegação entre as abas principais:

- `Navegando_Layout_Dash`, `Navegando_Layout_Base`
- `Navegando_Dash_Layout`, `Navegando_Dash_Base`
- `Navegando_Base_Layout`, `Navegando_Base_Dash`

Cada macro apenas seleciona a aba de destino — são atalhos de navegação para tornar a experiência do dashboard mais fluida (ex: botões clicáveis no `DashBoard` levando direto à base tratada).

---

## 7. Aba "Perguntas e Respostas"

Perguntas respondidas:

1. Quais categorias respondem pela maior parcela do faturamento total?
2. A média de desconto aplicada é adequada em relação ao faturamento?
3. O faturamento apresenta estabilidade ou volatilidade ao longo do período? *(usa a série real de 48 meses da aba `Aux_Mensal48`, não os 12 meses agregados de 4 anos — evita distorção no cálculo do desvio padrão)*
4. O ticket médio é compatível com o faturamento obtido?
5. O desempenho dos vendedores é equilibrado ou concentrado em poucos profissionais?
---

## 8. Como abrir e usar

1. Abra o arquivo no Excel e **habilite macros** quando solicitado.
2. Comece pela aba `DashBoard` para a visão executiva (KPIs + gráficos + slicers).
3. Use os slicers para filtrar por período, vendedor, categoria etc.
4. Veja `Perguntas e Respostas` para a análise de negócio detalhada.
5. Para investigar a base tratada, vá em `Base de Dados (Tratada)` (ou use a macro de navegação).
