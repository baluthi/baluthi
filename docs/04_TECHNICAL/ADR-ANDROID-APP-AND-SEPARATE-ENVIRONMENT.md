# ADR — Aplicativo Android e ambiente móvel separado

**Status:** Aprovado para Closed Beta  
**Data:** 2026-08-03  
**Responsável:** Documentação e arquitetura Baluthi

---

## 1. Contexto

A Baluthi possui uma aplicação web em Closed Beta e uma trilha separada de empacotamento e testes para Android.

O ambiente Android foi criado como uma cópia isolada para permitir testes nativos sem comprometer a disponibilidade, a segurança ou a integridade da versão beta. Essa separação não se limita ao APK ou ao processo de build: ela inclui banco de dados, autenticação, backend, armazenamento, credenciais, usuários e dados de teste.

A adoção do Android não altera o escopo funcional congelado do Closed Beta. O aplicativo móvel deve preservar as funcionalidades aprovadas para usuários comuns, enquanto o painel administrativo permanece exclusivamente na versão web.

---

## 2. Decisão

Foram aprovadas duas trilhas independentes de execução:

1. **Baluthi 2.0 / Closed Beta web** — fonte funcional principal, publicada pela Vercel e conectada ao ambiente beta.
2. **Aplicativo Android de teste** — cópia controlada para testes nativos, conectada exclusivamente ao ambiente móvel de testes.

O código funcional da versão Android deve acompanhar as correções aprovadas no Baluthi 2.0, mas os ambientes de dados e serviços não podem ser misturados.

A URL de teste móvel aprovada é `https://baluthi-mobile-poc.lovable.app`, ou outra URL que venha a substituí-la mediante atualização documental e validação formal. O aplicativo Android não pode apontar para o ambiente beta ou de produção.

---

## 3. Isolamento obrigatório

O ambiente Android deve manter, de forma integralmente separada da versão beta:

- URL da aplicação;
- banco de dados;
- autenticação;
- funções de backend e RPCs;
- armazenamento de comprovantes e anexos;
- credenciais e segredos;
- usuários e sessões;
- dados financeiros e registros de teste;
- e-mails transacionais;
- URLs permitidas de redirecionamento.

É proibido:

- reutilizar credenciais do ambiente beta no Android;
- copiar usuários, sessões ou dados reais para o ambiente móvel;
- executar testes Android contra o banco da versão beta;
- aplicar migrations diretamente em ambos os ambientes sem controle e registro separados;
- alterar manualmente apenas o projeto nativo quando a mudança pertence ao código funcional compartilhado.

Os testes Android devem utilizar somente dados fictícios.

---

## 4. Estratégia de sincronização de correções

O Baluthi 2.0 é a referência funcional e de código. A versão Android é uma derivação sincronizada de forma controlada.

Para cada correção ou pequeno lote de correções:

1. corrigir no Baluthi 2.0;
2. executar testes, typecheck e validação funcional na versão beta;
3. registrar o commit de origem;
4. replicar somente os arquivos e mudanças de código necessários para a versão Android;
5. aplicar migrations, funções RPC e ajustes de backend separadamente no ambiente Android;
6. confirmar que nenhuma variável ou credencial da versão beta foi copiada;
7. executar os testes específicos no Android;
8. registrar o resultado e os commits envolvidos antes de concluir o item.

Não é recomendado:

- manter duas implementações manuais independentes;
- corrigir os dois projetos simultaneamente sem uma origem definida;
- acumular muitas alterações e copiar novamente o projeto completo apenas ao final.

---

## 5. Fluxo de build aprovado

1. obter o código Android sincronizado com o commit aprovado do Baluthi 2.0;
2. confirmar as variáveis do ambiente móvel isolado;
3. instalar dependências;
4. executar typecheck, testes e build web;
5. executar o build móvel configurado no repositório;
6. sincronizar os artefatos com o projeto Android;
7. abrir o projeto no Android Studio;
8. compilar o APK de teste;
9. instalar em dispositivo de teste;
10. executar o plano de testes Android;
11. registrar versão, commits, ambiente, resultados e problemas conhecidos.

O comando exato de build móvel deve ser confirmado no `package.json` da versão usada. Não deve ser inferido quando ausente.

---

## 6. Regras de segurança

- Chaves de assinatura, senhas e arquivos de credenciais não devem ser versionados.
- APKs de teste não devem ser apresentados como publicação oficial na Play Store.
- O identificador atual do POC móvel deve permanecer distinto de uma futura versão oficial.
- Permissões de câmera, arquivos e armazenamento devem ser solicitadas somente quando necessárias.
- Acesso a anexos deve respeitar o isolamento entre usuários do ambiente Android.
- A versão móvel não pode contornar RLS, autenticação, RPCs ou controles do backend móvel.
- O painel administrativo permanece exclusivamente web; permissões administrativas continuam validadas no servidor.

---

## 7. Consequências

### Positivas

- proteção integral da base beta durante testes nativos;
- validação Android com dados fictícios;
- reaproveitamento controlado das correções do Baluthi 2.0;
- rastreabilidade entre correção, commit, migration e APK;
- redução do risco de divergência funcional.

### Custos e riscos

- necessidade de aplicar migrations separadamente em cada ambiente;
- necessidade de manter variáveis e credenciais móveis próprias;
- risco de divergência quando a sincronização de código não é realizada após cada lote;
- necessidade de testar permissões, teclado, botão voltar, anexos e conectividade;
- necessidade futura de assinatura, AAB e Play Console para distribuição oficial.

---

## 8. Critérios para publicação futura

Uma publicação na Play Store exige decisão adicional e, no mínimo:

- identificador definitivo do aplicativo;
- política de versionamento;
- chave de assinatura protegida e recuperável;
- geração de AAB;
- política de privacidade e ficha de segurança de dados;
- testes em dispositivos e versões Android representativos;
- processo de atualização e rollback;
- decisão formal sobre integração ou manutenção do backend móvel;
- aprovação formal da release.

---

## 9. Evidências pendentes

- confirmação, no repositório da aplicação, dos scripts e dependências móveis vigentes;
- registro das variáveis e identificadores do ambiente Android sem expor segredos;
- registro do primeiro APK aprovado, com commit e número de versão;
- execução completa do plano de testes Android;
- definição do processo técnico definitivo para sincronizar commits entre Baluthi 2.0 e a cópia Android;
- decisão sobre distribuição pela Play Store.
