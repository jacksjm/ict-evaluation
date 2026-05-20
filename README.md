# Indicador de Convergência Temporal (ICT)

[![Python 3.8+](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Status: Active](https://img.shields.io/badge/Status-Active-brightgreen)](https://github.com)

**Avaliação Dinâmica de Institutos de Pesquisa Eleitoral no Brasil**

---

## Resumo

O **Indicador de Convergência Temporal (ICT)** é uma ferramenta de ciência de dados para avaliar a confiabilidade de institutos de pesquisa eleitoral através da análise de sua dinâmica de convergência ou divergência em relação ao consenso agregado ao longo do período eleitoral.

Diferentemente de abordagens que focam apenas no erro final, o ICT captura a **trajetória temporal** de cada instituto, permitindo distinguir entre:

- **Convergência Esperada** (ICT > 0.05): Instituto converge para consenso
- **Comportamento Neutro** (-0.05 ≤ ICT ≤ 0.05): Instituto mantém padrão estável
- **Divergência Persistente** (ICT < -0.05): Instituto diverge do consenso

### Resultado Principal

A dinâmica temporal é um **preditor robusto de confiabilidade final**:
- **r = -0.883** (correlação muito forte)
- **R² = 0.779** (77.9% da variância explicada)
- **p = 0.001** (altamente significativo)

---

## Características Principais

### Rigor de Ciência de Dados
- Pipeline de 13 etapas com validação em múltiplos níveis
- Tratamento robusto de erros e casos extremos
- Logging completo para rastreabilidade
- Reproducibilidade garantida

### Metodologia Robusta
- Agregação ponderada baseada em variância binomial
- Ajustes de viés por método de coleta e tipo de pergunta
- Intervalos de confiança para todas as estimativas
- Testes estatísticos inferenciais (Shapiro-Wilk, Wilcoxon)

### Implementação Profissional
- Código bem documentado em Python
- Uso de bibliotecas especializadas (pandas, numpy, scipy)
- Exportação de resultados em múltiplos formatos (CSV, Excel, PNG)
- 13 gráficos avançados para visualização

### Transparência Científica
- Discussão explícita de limitações
- Validação estatística completa
- Código aberto e auditável
- Documentação técnica detalhada

---

## Dados e Resultados

### Base de Dados
- **Período:** 2022 (eleições presidenciais brasileiras)
- **Registros:** 4.600 pesquisas
- **Institutos:** 10 com ICT válido, 1 sem dado final
- **Duração:** ~6 meses (5 bimestres)
- **Qualidade:** Taxa de nulos < 2%

### Distribuição de Institutos
| Categoria | n | % | ICT Médio |
|-----------|---|---|-----------| 
| Convergência | 4 | 40% | 0.198 |
| Neutro | 2 | 20% | 0.025 |
| Divergência | 4 | 40% | -0.314 |

### Testes Estatísticos
| Teste | Resultado | p-valor | Conclusão |
|-------|-----------|---------|-----------|
| Shapiro-Wilk | W = 0.884 | 0.144 | Normal |
| Wilcoxon | W = 26 | 0.922 | Não significativo |
| Correlação | r = -0.883 | 0.001 | Altamente significativo |

---

## Quick Start

### Pré-requisitos
- Python 3.8+
- pip ou conda

### Instalação

```bash
# Clone o repositório
git clone https://github.com/jacksjm/ict-evaluation.git
cd ict-pesquisas-eleitorais

# Crie um ambiente virtual
python -m venv venv
source venv/bin/activate  # No Windows: venv\Scripts\activate

# Instale as dependências
pip install -r requirements.txt
```

### Execução

```bash
# Abra o Jupyter Notebook
jupyter notebook ICT_Metodologia_Melhorada.ipynb
```

### Saídas Geradas
- `saida_agregador_ict/resultado_ict_institutos.csv` - Resultados principais
- `saida_agregador_ict/distancias_por_instituto_bimestre.csv` - Dados bimestrais
- `saida_agregador_ict/consolidado_agregador_ict.xlsx` - Relatório Excel
- `saida_agregador_ict/ict_*.png` - 13 gráficos em alta resolução
- `saida_agregador_ict/notebook_execution.log` - Log de execução

---

## Estrutura do Repositório

```
ict-pesquisas-eleitorais/
├── README.md                                    # Este arquivo
├── requirements.txt                             # Dependências Python
└── ICT_Metodologia_Melhorada.ipynb             # Notebook principal
```

---

## Uso Avançado

### Personalizar Parâmetros

```python
# No notebook, modifique os parâmetros:
INTERVALO_BIMESTRES = 60  # dias
SHRINKAGE_MIN = 0.85      # limite inferior
SHRINKAGE_MAX = 1.15      # limite superior
TRUNCAMENTO_MIN = 0.001   # truncamento inferior
TRUNCAMENTO_MAX = 0.999   # truncamento superior
```

### Usar com Seus Dados

```python
# Prepare um CSV com as colunas:
# - data: data da pesquisa (YYYY-MM-DD)
# - instituto: nome do instituto
# - candidato: nome do candidato
# - percentual: percentual (0-1 ou 0-100)
# - tamanho_amostra: n da pesquisa
# - metodo: método de coleta (telefônico, online, presencial)
# - tipo_pergunta: tipo de pergunta (espontânea, estimulada)

# Coloque o arquivo em data/ e execute o notebook
```

---

## Gráficos Gerados

O notebook gera 13 gráficos em alta resolução (320 DPI):

1. **Série Temporal do ICT** - Evolução por instituto
2. **Violino por Categoria** - Distribuição do ICT
3. **Heatmap Instituto-Bimestre** - Matriz visual
4. **Dispersão ICT vs Distância** - Relação entre variáveis
5. **Barras de Classificação** - Ranking dos institutos
6. **Proporção Temporal** - Evolução das categorias
7. **Boxplot de Distâncias** - Variabilidade por instituto
8. **Agregador Diário** - Série temporal do consenso
9. **Histograma do ICT** - Distribuição de frequências
10. **Boxplot por Classe** - Comparação entre categorias
11. **Distância Inicial vs Final** - Relação entre períodos
12. **Heatmap Correlação** - Matriz de correlações
13. **Mapa de Calor Agregador** - Padrões espaço-temporais

---

## Validação e Testes

### Validação de Dados
- Verificação de valores nulos (< 5%)
- Validação de intervalo de percentuais (0-1)
- Cobertura temporal mínima (30 dias)
- Número mínimo de institutos e candidatos
- Detecção de duplicatas

### Testes Estatísticos
- Shapiro-Wilk para normalidade
- Wilcoxon signed-rank para significância
- Pearson para correlação
- Verificação de intervalos de confiança

### Garantia de Qualidade
- Pesos válidos (> 0)
- Somas ponderadas finitas
- Intervalos de confiança ordenados
- p-valores em [0, 1]
- Gráficos sem erros de renderização

---

## Complexidade Computacional

| Etapa | Operação | Complexidade | Tempo |
|-------|----------|--------------|-------|
| Validação | O(n) | 1-2s |
| Agregação | O(n log n) | 3-5s |
| Testes | O(i) | 1-2s |
| Gráficos | O(n) | 30-45s |
| **Total** | **O(n log n)** | **2-3 min** |

Onde n ≈ 4.600 registros, i ≈ 10 institutos

---

## Limitações

1. **Truncamento de Percentuais:** Valores extremos são truncados em [0.001, 0.999]
2. **Shrinkage de Pesos:** Intervalo [0.85, 1.15] é arbitrário
3. **Bimestres Fixos:** Intervalo de 60 dias pode ser inadequado para períodos com poucos dados
4. **Tamanho Amostral:** Com apenas ~10 institutos, poder estatístico pode ser limitado
5. **Independência:** Assume que institutos não são correlacionados

---

## Trabalhos Futuros

- [ ] Análise de sensibilidade (variar parâmetros)
- [ ] Comparação com agregadores alternativos
- [ ] Modelagem temporal (ARIMA, suavização exponencial)
- [ ] Análise de clusters (agrupar institutos similares)
- [ ] Integração com Machine Learning (prever acurácia)
- [ ] Aplicação em outros ciclos eleitorais
- [ ] Extensão para bases com maior heterogeneidade

---

## Tecnologias Utilizadas

| Tecnologia | Versão | Uso |
|-----------|--------|-----|
| Python | 3.8+ | Linguagem principal |
| pandas | 1.3+ | Manipulação de dados |
| numpy | 1.20+ | Operações numéricas |
| scipy | 1.7+ | Testes estatísticos |
| matplotlib | 3.4+ | Visualização |
| seaborn | 0.11+ | Gráficos estatísticos |
| openpyxl | 3.6+ | Exportação Excel |
| Jupyter | 1.0+ | Ambiente interativo |

---

## Citação

Se usar este trabalho, cite como:

```bibtex
@article{schweitzer2022ict,
  title={Indicador de Convergência Temporal para Avaliação Dinâmica de Institutos de Pesquisa Eleitoral no Brasil},
  author={Schweitzer, Dayane da Silva Xavier and Machado, Jackson},
  journal={[Revista/Conferência]},
  year={2022},
  institution={Universidade do Estado de Santa Catarina (UDESC)}
}
```

---

## Licença

Este projeto está licenciado sob a [MIT License](LICENSE) - veja o arquivo LICENSE para detalhes.

---

## Autores

- **Dayane da Silva Xavier Schweitzer** - UDESC
- **Jackson Machado** - UDESC

---

## Contribuições

Contribuições são bem-vindas! Por favor:

1. Fork o projeto
2. Crie uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
3. Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. Push para a branch (`git push origin feature/AmazingFeature`)
5. Abra um Pull Request

---

## Agradecimentos

- Universidade do Estado de Santa Catarina (UDESC)
- Institutos de pesquisa que forneceram dados
- Comunidade de ciência de dados Python

---

## Referências

1. Shirani-Mehr, H., Rothschild, D., Goel, S., & Gelman, A. (2018). "Disentangling bias and variance in election polls." *Journal of the American Statistical Association*, 113(522), 607-614.

2. Jackman, S. (2005). "Pooling the polls over an election campaign." *Australian Journal of Political Science*, 40(4), 499-517.

3. Linzer, D. A. (2013). "Dynamic Bayesian forecasting of presidential elections in the states." *Journal of the American Statistical Association*, 108(501), 124-134.

4. Pew Research Center. (2015). "From telephone to the web: The challenge of mode effects in public opinion polls." *Pew Research Center Technical Report*.

5. McKinney, W. (2010). "Data Structures for Statistical Computing in Python." *Proceedings of the 9th Python in Science Conference*, 445, 51-56.

---

## Status do Projeto

- [X] Implementação completa
- [X] Testes estatísticos
- [X] Documentação técnica
- [X] Artigo científico
- [ ] **[EM EXECUÇÃO]** Preparação para publicação
- [ ] Extensões futuras

---

**⭐ Se este projeto foi útil, considere dar uma estrela!**
