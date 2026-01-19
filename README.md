# ⚡ Inteligência Geoespacial em Redes de Distribuição (CPFL Piratininga)

> Projeto desenvolvido pela equipe **Cognição Elétrica** durante o **Hackathon Radix**.

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Geopandas](https://img.shields.io/badge/Geospatial-Geopandas-green)
![Folium](https://img.shields.io/badge/Viz-Folium-orange)
![Status](https://img.shields.io/badge/Status-Concluído-success)

## 📄 Sobre o Projeto

Este projeto visa resolver a "cegueira de dados" em redes de distribuição de energia elétrica. Utilizando dados abertos da ANEEL (BDGD), desenvolvemos um pipeline de engenharia de dados capaz de transformar arquivos brutos (`.gdb`) em inteligência visual estratégica.

O foco principal foi mapear a rede da **CPFL Piratininga**, identificando perfis de consumo e a penetração de Geração Distribuída (Solar) para apoiar tomadas de decisão sobre expansão de rede e novos negócios.

### 🎯 O Desafio
Em bases de dados elétricos, o volume massivo de unidades residenciais tende a "esconder" estatisticamente os polos comerciais e industriais. Uma contagem simples indicaria que quase todas as subestações são residenciais, o que não reflete a realidade da carga e da importância econômica da região.

## 🛠️ A Solução Técnica

Desenvolvemos uma **Lógica Hierárquica de Relevância** para classificação de áreas, ignorando a contagem absoluta e focando no impacto da carga.

### Funcionalidades Principais:
1.  **Processamento de GDB:** Leitura direta de Geodatabases da ANEEL (camadas `SSDMT`, `SUB`, `UCBT`, `UGBT`) sem necessidade de conversão externa.
2.  **Classificação Inteligente:** Algoritmo que categoriza subestações/conjuntos em:
    * 🟣 **Industrial:** Se houver > 1% de unidades industriais.
    * 🔴 **Comercial:** Se houver > 10% de unidades comerciais.
    * 🔵 **Residencial:** Se houver > 90% de unidades residenciais.
    * 🟠 **Misto:** Áreas de alta densidade urbana mista.
3.  **Cálculo de Densidade GD:** Métrica de $kW/km^2$ para identificar saturação ou oportunidade para energia solar.
4.  **Mapa Interativo:** Visualização em HTML com filtros de camadas e tooltips detalhados para auditoria de dados.

## 🚀 Tecnologias Utilizadas

* **Linguagem:** Python
* **Processamento Geoespacial:** Geopandas, Fiona, Shapely
* **Manipulação de Dados:** Pandas
* **Visualização:** Folium (Mapas Interativos)
* **Ambiente de Desenvolvimento:** Google Colab

## 📊 Metodologia e Pipeline

O projeto segue um pipeline ETL (Extract, Transform, Load):

1.  **Extract:** Extração automática de geometrias e tabelas do arquivo `.gdb`.
2.  **Transform:**
    * Limpeza de dados e tratamento de nulos.
    * Cálculo estatístico de consumidores por classe (`UCBT`).
    * Soma de potência instalada de Geração Distribuída (`UGBT`).
    * Aplicação da Lógica Hierárquica.
    * Junção espacial (Merge) baseada nos códigos de Conjuntos/Subestações.
3.  **Load/Viz:** Geração de arquivo `.html` interativo com camadas de controle.

## 📦 Como Executar

Este projeto foi otimizado para rodar no **Google Colab**.

1.  Clone este repositório.
2.  Faça o upload do notebook `.ipynb` no Google Colab.
3.  Certifique-se de ter o arquivo da base de dados (ex: `CPFL_Piratininga.gdb`) zipado ou descompactado no ambiente.
4.  Instale as dependências necessárias:

```python
!pip install geopandas fiona folium
