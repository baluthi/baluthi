# ADR — Aplicativo Android e ambiente móvel separado

**Status:** Aprovado para Closed Beta  
**Data:** 2026-08-03  
**Responsável:** Documentação e arquitetura Baluthi

---

## 1. Contexto

A Baluthi possui aplicação web em produção e passou a ter uma trilha de empacotamento e testes para Android. Os testes móveis precisam ocorrer sem comprometer a disponibilidade ou a integridade do ambiente web utilizado pelos demais usuários.

A adoção do Android não altera o escopo funcional congelado do Closed Beta. O aplicativo móvel deve expor as mesmas funcionalidades aprovadas para a aplicação web, salvo limitações móveis documentadas.

---

## 2. Decisão

Foi aprovada a manutenção de duas trilhas de execução:

1. **Web de produção** — publicada pela Vercel e acessada por navegador.
2. **Aplicativo Android de teste** — gerado por processo de build móvel, aberto e compilado no Android Studio e distribuído inicialmente como APK fora da Play Store.

O código funcional deve permanecer originado do repositório oficial da aplicação. Alterações específicas do Android não podem criar uma segunda implementação independente das regras financeiras.

---

## 3. Separação de ambientes

A expressão “ambiente separado” deve ser descrita explicitamente em cada release móvel. A documentação da versão deve informar se a separação abrange:

- apenas o artefato e o processo de build;
- URL da aplicação;
- banco de dados;
- autenticação;
- armazenamento de comprovantes;
- funções de backend;
- credenciais e segredos;
- URLs permitidas de redirecionamento.

Enquanto não houver evidência de isolamento próprio de backend, o aplicativo Android deve ser tratado como potencial consumidor dos mesmos serviços utilizados pela web. Nenhuma documentação pode afirmar isolamento de dados sem validação técnica.

---

## 4. Fluxo aprovado

O fluxo operacional aprovado é:

1. obter o código da versão a ser testada;
2. instalar dependências;
3. executar typecheck, testes e build web;
4. executar o build móvel configurado no repositório;
5. sincronizar os artefatos web com o projeto Android;
6. abrir o projeto no Android Studio;
7. compilar APK de teste;
8. instalar em dispositivo de teste;
9. executar o plano de testes Android;
10. registrar versão, commit, ambiente, resultados e problemas conhecidos.

O comando exato de build móvel deve ser confirmado no `package.json` da versão usada. Não deve ser inferido quando ausente.

---

## 5. Regras de segurança

- Chaves de assinatura, senhas e arquivos de credenciais não devem ser versionados.
- APKs de teste não devem ser apresentados como publicação oficial na Play Store.
- O pacote deve ser testado com conta e dados fictícios sempre que houver risco de exposição.
- Permissões de câmera, arquivos e armazenamento devem ser solicitadas somente quando necessárias.
- Acesso a anexos deve respeitar o isolamento entre usuários.
- A versão móvel não pode contornar RLS, autenticação, RPCs ou controles existentes no backend.

---

## 6. Consequências

### Positivas

- validação da experiência Android sem substituir a aplicação web;
- possibilidade de testes controlados com APK;
- reaproveitamento do núcleo funcional existente;
- rastreabilidade entre versão web, commit e artefato Android.

### Custos e riscos

- necessidade de manter configuração nativa e dependências Android;
- risco de divergência entre o código web e o projeto nativo;
- necessidade de testar permissões, teclado, botão voltar, anexos e conectividade;
- risco de o aplicativo de teste acessar o ambiente incorreto;
- necessidade futura de assinatura, AAB e Play Console para distribuição oficial.

---

## 7. Critérios para publicação futura

Uma publicação na Play Store exige decisão adicional e, no mínimo:

- identificador definitivo do aplicativo;
- política de versionamento;
- chave de assinatura protegida e recuperável;
- geração de AAB;
- política de privacidade e ficha de segurança de dados;
- testes em dispositivos e versões Android representativos;
- processo de atualização e rollback;
- aprovação formal da release.

---

## 8. Evidências pendentes

- confirmação, no repositório da aplicação, dos scripts e dependências móveis vigentes;
- definição inequívoca do backend utilizado pelo APK;
- registro do primeiro APK aprovado, com commit e número de versão;
- execução completa do plano de testes Android;
- decisão sobre distribuição pela Play Store.
