# Automação e Consolidação de Métricas de Vendas (Excel to Python) 🚀

Este repositório contém um projeto de Engenharia de Dados desenvolvido para automatizar a geração da "Tabela Geral de Vendas". O objetivo principal é substituir um processo manual complexo e pesado, realizado anteriormente via fórmulas de Excel, por um pipeline de dados robusto e performático utilizando Python.

## 🎯 Objetivo do Projeto
Atualmente, a consolidação dos dados de vendas envolve baixar relatórios de diversas fontes (VTEX, ERPs, GA4) e cruzá-los em planilhas pesadas. Este projeto visa:
1.  **Automatizar a ingestão** de dados de múltiplas fontes.
2.  **Replicar e otimizar regras de negócio** (categorização, cálculo de frete, regras de cancelamento) usando Pandas.
3.  **Aumentar a performance**, reduzindo o tempo de processamento e eliminando travamentos comuns no Excel.
4.  **Gerar uma base unificada** (Dataset) pronta para análise em BI.

## 🛠️ Tecnologias Utilizadas
* **Python**
* **Pandas:** Manipulação e transformação de dados massivos.
* **NumPy:** Vetorização de condições lógicas complexas.
* **Jupyter Notebook:** Ambiente de desenvolvimento e documentação do código.

## 🔄 Arquitetura do Pipeline (ETL)

### 1. Extração (Extract)
O script lê dados de formatos heterogêneos provenientes de diferentes sistemas:
* **VTEX (CSV):** Dados transacionais brutos de vendas.
* **USE (HTML/XLS):** Relatórios operacionais de pedidos.
* **Sankhya (XLSX):** Dados do ERP para validação de corte/estoque.
* *Em breve: Integração com dados de mídia (GA4).*

### 2. Transformação (Transform)
Esta é a etapa onde as "fórmulas do Excel" são convertidas em código Python eficiente:
* **Limpeza de Dados:** Tratamento de tipos (datetime, string), formatação de telefones e normalização de CPFs.
* **Engenharia de Atributos (Feature Engineering):**
    * Criação de IDs únicos compostos (`Pedido` + `SKU` + `Tamanho`) para cruzamento de bases.
    * Categorização automática de produtos (Ex: Sapatos, Bolsas, Acessórios) baseada em listas de palavras-chave.
    * Mapeamento geográfico (Regiões baseadas em UF).
    * Definição de modelo de negócio (Loja, CD, Outlet).
* **Lógica Avançada de Cancelamento:**
    * Cruza informações de três fontes (Status VTEX, Relatório USE e Relatório Sankhya).
    * Utiliza lógica de conjuntos (`set` e `isin`) para identificar itens cancelados ou cortados com performance O(1), substituindo `VLOOKUPs` lentos.

### 3. Carga (Load)
* Exportação da base consolidada e tratada (atualmente em Excel/XLSX para validação, com planos para Parquet/SQL).

## 🚧 Status do Projeto
* [x] Ingestão e Limpeza VTEX.
* [x] Regras de Categorização de Produtos e Clientes.
* [x] Lógica unificada de Cancelamentos (Sankhya + USE + VTEX).
* [ ] Integração com dados do GA4 (Mídia).
* [ ] Otimização da exportação final.
