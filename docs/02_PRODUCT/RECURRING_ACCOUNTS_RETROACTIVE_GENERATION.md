# Contas recorrentes — geração retroativa de compromissos

**Status:** Regra aprovada e implementada  
**Data:** 2026-08-03  
**Aplicação:** Baluthi 2.0 / Closed Beta web

---

## 1. Regra funcional

Ao criar uma conta recorrente com **Data de início** anterior à data atual, o sistema deve materializar os compromissos desde a data informada até o horizonte de geração vigente.

O comportamento deve ser idêntico nos dois caminhos de criação:

- `Lançamentos`;
- `Mais > Contas recorrentes`.

A origem da série é sempre `data_inicio`. Não é permitido iniciar a geração apenas no mês atual quando a data cadastrada for retroativa.

---

## 2. Limites e proteção contra duplicidade

A geração deve:

- respeitar `data_fim` quando informada;
- respeitar `ocorrencias_max` quando informado;
- respeitar a frequência e o intervalo configurados;
- não recriar ocorrências já materializadas;
- não recriar datas registradas como exceções ou removidas da série;
- não gerar ocorrências para séries inativas;
- preservar lançamentos já pagos ou individualmente alterados;
- utilizar somente a série pertencente ao usuário autenticado.

---

## 3. Fluxo técnico aprovado

### Criação

A criação por `Mais > Contas recorrentes` deve utilizar a mesma RPC `criar_serie_fixa` utilizada pelo fluxo `Lançamentos`.

Essa RPC cria o cadastro da recorrência e aciona a geração das ocorrências a partir de `data_inicio`.

### Edição

Após editar uma série, o sistema deve executar `sincronizar_serie_recorrente(_serie_id, _meses)`.

A função:

- valida a sessão;
- confirma que a série pertence ao usuário autenticado;
- chama a geração existente;
- completa somente as ocorrências ausentes;
- não duplica ocorrências existentes.

A sincronização não remove automaticamente compromissos antigos quando a série é encurtada. Exclusões ou alterações retroativas devem seguir o fluxo próprio de edição/cancelamento da série para preservar histórico e auditabilidade.

---

## 4. Atualização de interface

Após criar ou editar uma conta recorrente, devem ser atualizadas as consultas de:

- contas recorrentes;
- lançamentos;
- faturas, quando aplicável;
- dashboard.

Isso garante que os compromissos gerados apareçam imediatamente sem exigir novo login ou recarregamento manual.

---

## 5. Segurança

A RPC `sincronizar_serie_recorrente` é `SECURITY DEFINER`, com `search_path` controlado e validação explícita por `auth.uid()`.

Permissões:

- `authenticated`: permitido;
- `service_role`: permitido;
- `anon`: negado;
- `PUBLIC`: negado.

---

## 6. Evidências da implementação

Commit da aplicação:

```text
d5bf4c4e152e9fb9a6688a04b603988a1c6dcdcb
```

Arquivos principais:

- `src/lib/api.ts`;
- `src/lib/serie-ocorrencias.ts`;
- `tests/serie-ocorrencias.test.ts`;
- migration com `sincronizar_serie_recorrente`.

Validações registradas:

- 185 testes aprovados;
- 12 testes novos para recorrências;
- typecheck aprovado;
- build aprovado;
- sem alteração no ambiente Android isolado.

---

## 7. Sincronização futura com Android

Esta correção foi aplicada somente no Baluthi 2.0.

Ao sincronizar para o Android:

1. replicar o código correspondente;
2. aplicar a RPC separadamente no banco Android;
3. não copiar URL, credenciais ou dados do ambiente beta;
4. executar novamente os testes de recorrência no ambiente Android isolado;
5. registrar commits, migration e resultados na release Android.
