# Registro de release Android — Closed Beta

**Status:** Modelo ativo  
**Data de criação:** 2026-08-03

---

## 1. Finalidade

Este documento deve ser atualizado a cada APK destinado a testes. Ele identifica exatamente o código, o ambiente isolado e as evidências que originaram o artefato.

O APK Android não pode utilizar banco, autenticação, backend, armazenamento, credenciais, usuários ou dados da versão beta.

---

## 2. Identificação da release

Preencher antes da distribuição:

| Campo | Valor |
|---|---|
| Versão do aplicativo | Pendente |
| Número do build | Pendente |
| Data e hora | Pendente |
| Commit da cópia Android | Pendente |
| Commit correspondente do Baluthi 2.0 | Pendente |
| Branch/projeto Android | Pendente |
| Nome do APK | Pendente |
| Hash do APK | Pendente |
| Tipo de build | Debug/teste |
| Responsável | Pendente |

---

## 3. Ambiente Android isolado

| Componente | Ambiente/identificação |
|---|---|
| URL carregada pelo app | `https://baluthi-mobile-poc.lovable.app` ou substituta formalmente aprovada |
| Banco de dados Android | Pendente |
| Autenticação Android | Pendente |
| Armazenamento de anexos Android | Pendente |
| Funções de backend/RPCs Android | Pendente |
| E-mails transacionais Android | Pendente |
| URLs de redirecionamento Android | Pendente |
| Credenciais/segredos Android | Confirmar separação sem registrar valores |
| Usuários e dados utilizados | Somente fictícios |

A release não pode ser distribuída enquanto esses campos permanecerem ambíguos.

Também deve ser confirmado expressamente:

- [ ] nenhuma URL do ambiente beta está configurada;
- [ ] nenhuma credencial beta foi reutilizada;
- [ ] nenhum usuário, sessão ou dado beta está presente;
- [ ] nenhuma migration foi aplicada por engano no banco beta;
- [ ] nenhum anexo Android é armazenado no ambiente beta.

---

## 4. Sincronização com Baluthi 2.0

Registrar cada lote de correções replicado:

| Item | Commit Baluthi 2.0 | Commit/cópia Android | Migration/RPC Android | Resultado |
|---|---|---|---|---|
| Pendente | Pendente | Pendente | Pendente | Pendente |

Regra de processo:

1. corrigir e validar no Baluthi 2.0;
2. registrar o commit de origem;
3. replicar a mudança para a cópia Android;
4. aplicar alterações de banco separadamente no ambiente Android;
5. testar no Android;
6. concluir somente após registrar evidências.

---

## 5. Validações de build

- [ ] dependências instaladas sem alteração não documentada;
- [ ] typecheck aprovado;
- [ ] testes automatizados aprovados;
- [ ] build web aprovado;
- [ ] build móvel aprovado;
- [ ] sincronização Android concluída;
- [ ] Gradle sincronizado;
- [ ] APK instalado em dispositivo físico;
- [ ] ausência de chaves ou segredos versionados;
- [ ] isolamento do ambiente Android validado.

---

## 6. Testes executados

Referência obrigatória: `docs/05_QA/ANDROID_CLOSED_BETA_TEST_PLAN.md`.

| Área | Resultado | Evidência/observação |
|---|---|---|
| Instalação e inicialização | Pendente | |
| Isolamento beta x Android | Pendente | |
| Autenticação | Pendente | |
| Navegação | Pendente | |
| Formulários e teclado | Pendente | |
| Regras financeiras | Pendente | |
| Sincronização das correções | Pendente | |
| Anexos e permissões | Pendente | |
| Rede e resiliência | Pendente | |
| Relatórios e PDF | Pendente | |
| Segurança e isolamento entre usuários | Pendente | |

---

## 7. Dispositivos testados

| Modelo | Android | Resultado | Observações |
|---|---|---|---|
| Pendente | Pendente | Pendente | |

---

## 8. Correções incluídas

Registrar commits e correções relevantes incluídas no build. Não utilizar descrições genéricas.

- Pendente.

---

## 9. Migrations e backend Android

Registrar exclusivamente alterações aplicadas ao ambiente Android:

| Migration/RPC | Origem | Data de aplicação | Resultado | Evidência |
|---|---|---|---|---|
| Pendente | Pendente | Pendente | Pendente | Pendente |

Nenhuma aplicação no ambiente beta deve ocorrer como consequência automática desta release.

---

## 10. Problemas conhecidos

- Pendente.

Qualquer conexão com a versão beta, mistura de dados, falha de segurança, perda de dados, autenticação ou inconsistência financeira bloqueia a distribuição até correção.

---

## 11. Distribuição

- Canal: APK de teste fora da Play Store.
- Público: grupo controlado de testes Android.
- Dados: exclusivamente fictícios.
- Orientação: não encaminhar o APK para terceiros não autorizados.
- Play Store: não publicada nesta fase.

---

## 12. Rollback

Em caso de falha grave:

1. interromper a distribuição;
2. comunicar os testadores;
3. remover ou desabilitar o artefato afetado;
4. orientar retorno à versão Android anterior ou à aplicação web beta, sem transferir dados entre ambientes;
5. preservar evidências;
6. corrigir e gerar nova versão com outro número de build.

---

## 13. Aprovação final

| Papel | Nome | Data | Decisão |
|---|---|---|---|
| Produto | Pendente | Pendente | Pendente |
| Técnico/QA | Pendente | Pendente | Pendente |

O preenchimento deste documento faz parte da própria release e não é uma atividade opcional posterior.
