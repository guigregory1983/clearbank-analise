# ClearBank — Análise Financeira com Python

Desafio final do módulo de Python aplicado à análise de dados. O projeto lê o
histórico mensal de transações de uma fintech fictícia (a **ClearBank**),
valida e limpa os dados, calcula métricas financeiras por mês, sinaliza
transações suspeitas, exibe um relatório formatado no terminal e exporta o
resultado em JSON.

## Estrutura do repositório

```
clearbank-analise/
├── desafio-final.ipynb   # notebook principal (código + saídas salvas)
├── transacoes.csv        # dados de entrada (1000 registros)
├── analise_pandas.py     # (opcional · RO1) versão alternativa com pandas
├── grafico.png           # (opcional · RO2) crédito x débito por mês
├── relatorio.json        # saída gerada pelo notebook
└── README.md
```

## Dados de entrada

`transacoes.csv` contém **1000 registros**: 750 válidos, 250 inválidos (cobrindo
os 5 tipos de erro tratados na validação) e 100 transações acima de R$ 10.000,
distribuídos entre janeiro e junho de 2026.

| Coluna | Tipo | Regra de validação |
|---|---|---|
| id | inteiro | único, numérico, não vazio |
| data | texto | formato `AAAA-MM-DD` |
| cliente_id | texto | não pode ser vazio |
| tipo | texto | exatamente `credito` ou `debito` |
| valor | decimal | maior que 0 |
| descricao | texto | livre |
| categoria | texto | livre |

## Como executar

### Google Colab
1. Faça upload de `desafio-final.ipynb` e de `transacoes.csv`.
2. Menu **Runtime → Run all** (ou rode as células em ordem, de cima para baixo).

### Jupyter Notebook (local)
1. Requer **Python 3.10+**. Para os opcionais: `pip install pandas matplotlib`.
2. Mantenha `transacoes.csv` na mesma pasta do notebook.
3. Abra o notebook e execute todas as células em ordem.

> Importante: rode as células **na ordem**. A última (*Célula de Execução
> Principal*) chama todas as funções e produz o relatório final + o JSON.

## O que o notebook gera

- **No terminal**: resumo da limpeza (linhas lidas / válidas / inválidas),
  o período analisado, o relatório mensal (quantidade, crédito, débito, saldo,
  média, maior e menor valor por mês) e a lista de transações suspeitas.
- **`relatorio.json`**: arquivo com `gerado_em`, totais de transações válidas e
  inválidas, o resumo mensal e as transações suspeitas.
- **`grafico.png`** (opcional): barras empilhadas de crédito e débito por mês.

## Opcionais implementados

- **RO1 — pandas** (`analise_pandas.py`): recalcula as métricas com
  `pd.read_csv` + `groupby` e compara com o `relatorio.json` da solução nativa.
  Rode com `python analise_pandas.py` após gerar o `relatorio.json` pelo
  notebook. Os valores conferem integralmente.
- **RO2 — matplotlib**: gráfico de barras empilhadas (`grafico.png`) com título,
  rótulos nos eixos e legenda, gerado na última seção do notebook.
