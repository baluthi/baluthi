# Registro de release Android — Closed Beta

**Status:** Modelo ativo  
**Data de criação:** 2026-08-03

---

## 1. Finalidade

Este documento deve ser atualizado a cada APK destinado a testes. Ele identifica exatamente o código, o ambiente e as evidências que originaram o artefato.

---

## 2. Identificação da release

Preencher antes da distribuição:

| Campo | Valor |
|---|---|
| Versão do aplicativo | Pendente |
| Número do build | Pendente |
| Data e hora | Pendente |
| Commit de origem | Pendente |
| Branch | Pendente |
| Nome do APK | Pendente |
| Hash do APK | Pendente |
| Tipo de build | Debug/teste |
| Responsável | Pendente |

---

## 3. Ambiente

| Componente | Ambiente/identificação |
|---|---|
| URL carregada pelo app | Pendente |
| Banco de dados | Pendente |
| Autenticação | Pendente |
| Armazenamento de anexos | Pendente |
| Funções de backend | Pendente |
| E-mails transacionais | Pendente |
| URLs de redirecionamento | Pendente |

A release não pode ser distribuída enquanto esses campos permanecerem ambíguos.

---

## 4. Validações de build

- [ ] dependências instaladas sem alteração não documentada;
- [ ] typecheck aprovado;
- [ ] testes automatizados aprovados;
- [ ] build web aprovado;
- [ ] build móvel aprovado;
- [ ] sincronização Android concluída;
- [ ] Gradle sincronizado;
- [ ] APK instalado em dispositivo físico;
- [ ] ausência de chaves ou segredos versionados.

---

## 5. Testes executados

Referência obrigatória: `docs/05_QA/ANDROID_CLOSED_BETA_TEST_PLAN.md`.

| Área | Resultado | Evidência/observação |
|---|---|---|
| Instalação e inicialização | Pendente | |
| Autenticação | Pendente | |
| Navegação | Pendente | |
| Formulários e teclado | Pendente | |
| Regras financeiras | Pendente | |
| Anexos e permissões | Pendente | |
| Rede e resiliência | Pendente | |
| Relatórios e PDF | Pendente | |
| Segurança e isolamento | Pendente | |

---

## 6. Dispositivos testados

| Modelo | Android | Resultado | Observações |
|---|---|---|---|
| Pendente | Pendente | Pendente | |

---

## 7. Correções incluídas

Registrar commits e correções relevantes incluídas no build. Não utilizar descrições genéricas.

- Pendente.

---

## 8. Problemas conhecidos

- Pendente.

Qualquer falha de segurança, perda de dados, autenticação ou inconsistência financeira bloqueia a distribuição até correção ou decisão formal.

---

## 9. Distribuição

- Canal: APK de teste fora da Play Store.
- Público: grupo controlado do Closed Beta.
- Orientação: não encaminhar o APK para terceiros não autorizados.
- Play Store: não publicada nesta fase.

---

## 10. Rollback

Em caso de falha grave:

1. interromper a distribuição;
2. comunicar os testadores;
3. remover ou desabilitar o artefato afetado;
4. orientar retorno à versão anterior ou à aplicação web;
5. preservar evidências;
6. corrigir e gerar nova versão com outro número de build.

---

## 11. Aprovação final

| Papel | Nome | Data | Decisão |
|---|---|---|---|
| Produto | Pendente | Pendente | Pendente |
| Técnico/QA | Pendente | Pendente | Pendente |

O preenchimento deste documento faz parte da própria release, e não é uma atividade opcional posterior.
