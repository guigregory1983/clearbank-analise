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

## Exemplo de saída no terminal

```
========================================
       ANÁLISE FINANCEIRA — ClearBank
========================================
Período analisado: 2026-01-01 → 2026-06-30 (180 dias)
Transações válidas:   750
Transações inválidas: 250

===== RELATÓRIO MENSAL =====

Mês: 2026-01
  Transações:    116
  Total crédito: R$ 298.131,28
  Total débito:  R$ 475.698,90
  Saldo:         R$ -177.567,62
  Média:         R$ 6.670,95
  Maior valor:   R$ 55.895,10
  Menor valor:   R$ 188,84
...

===== TRANSAÇÕES SUSPEITAS =====
ID: 723 | Cliente: CLI037 | Data: 2026-01-02 | Valor: R$ 16.161,77
...
```

