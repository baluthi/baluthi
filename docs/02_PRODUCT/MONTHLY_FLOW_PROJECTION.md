# Fluxo mensal — realizado e projetado

**Status:** Implementado no Baluthi 2.0  
**Data:** 2026-08-03  
**Escopo:** Dashboard do usuário

---

## 1. Objetivo

O gráfico de Fluxo mensal deve permitir que o usuário compreenda tanto o histórico efetivo quanto a disponibilidade financeira projetada para os próximos meses.

---

## 2. Regra de exibição

- **Meses passados:** mostram somente valores realizados, considerando receitas recebidas e despesas pagas.
- **Mês atual:** mostra uma visão híbrida, composta pelo realizado até a data atual e pelo previsto para o restante do mês.
- **Meses futuros:** mostram projeções de receitas e despesas previstas.
- **Saldo:** apresenta o saldo acumulado projetado, partindo do saldo atual das contas e encadeando o resultado de cada mês.

O gráfico possui regra própria e não depende do seletor global Caixa/Competência.

---

## 3. Fontes consideradas

### Realizado

- lançamentos pagos;
- valor efetivo do lançamento, incluindo descontos, juros ou multas;
- data de pagamento;
- pagamento de fatura de cartão, evitando somar também as compras que compõem a fatura.

### Previsto

- lançamentos pendentes, agendados ou vencidos pela data de vencimento;
- parcelas futuras já cadastradas;
- recorrências já materializadas;
- recorrências futuras projetadas em memória, sem gravação adicional no banco;
- saldo devedor de faturas de cartão em aberto na data de vencimento.

---

## 4. Exclusões obrigatórias

Não entram no gráfico:

- transferências entre contas;
- lançamentos cancelados;
- estornos;
- compras de cartão quando a fatura correspondente já representa a obrigação;
- registros duplicados de recorrências;
- qualquer valor de outro usuário.

---

## 5. Representação visual

O gráfico deve distinguir claramente:

- valores realizados;
- valores previstos;
- mês atual parcial;
- saldo acumulado projetado.

A legenda e o tooltip devem informar o modo do mês e separar os valores realizados dos previstos.

---

## 6. Critérios de aceitação

- mês passado ignora valores ainda não pagos;
- mês futuro considera obrigações e receitas previstas;
- mês atual não duplica valores já realizados;
- faturas de cartão não geram dupla contagem;
- transferências não alteram resultado patrimonial;
- recorrências futuras aparecem no horizonte do gráfico sem criar novos registros no banco;
- saldo projetado é acumulado a partir do saldo atual;
- comportamento possui cobertura automatizada.

---

## 7. Evidência de implementação

Implementação no repositório `baluthi/baluthi-com`:

- commit `b49814a5966dd2f419176f427047977b8c753f2f`;
- novo motor em `src/lib/fluxo.ts`;
- dashboard atualizado em `src/routes/_authenticated/dashboard.tsx`;
- testes em `tests/fluxo-mensal.test.ts`;
- 174 testes aprovados;
- typecheck, lint e build aprovados;
- nenhuma migration criada.

---

## 8. Android

Esta alteração foi implementada somente no Baluthi 2.0. A replicação para o ambiente Android deve ocorrer em lote controlado, preservando banco de dados, autenticação, backend, armazenamento e credenciais Android totalmente separados da versão beta.
