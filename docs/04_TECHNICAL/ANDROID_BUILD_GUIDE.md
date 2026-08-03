# Guia de build Android — Baluthi

**Status:** Ativo para testes do Closed Beta  
**Data:** 2026-08-03

---

## 1. Objetivo

Padronizar a geração do aplicativo Android de teste da Baluthi, evitando divergências entre máquinas, builds e ambientes.

Este guia não autoriza publicação na Play Store. O artefato atual é destinado a testes controlados e deve permanecer conectado exclusivamente ao ambiente Android isolado.

---

## 2. Princípio obrigatório de isolamento

O aplicativo Android de teste não pode utilizar o banco de dados, autenticação, backend, armazenamento, credenciais, usuários ou dados da versão beta.

A URL móvel atualmente aprovada é:

```text
https://baluthi-mobile-poc.lovable.app
```

Qualquer alteração dessa URL ou do backend correspondente exige validação e atualização documental antes do build.

Os testes devem utilizar somente contas e dados fictícios.

---

## 3. Pré-requisitos

Antes de iniciar, confirmar:

- acesso ao código da versão Android;
- commit do Baluthi 2.0 que originou a sincronização;
- Node.js e gerenciador de pacotes compatíveis com o projeto;
- Java/JDK compatível com a versão do Android Gradle Plugin;
- Android Studio atualizado e SDK Android instalado;
- dispositivo físico ou emulador disponível;
- variáveis de ambiente exclusivas do ambiente Android;
- ausência de chaves, senhas ou arquivos de assinatura no Git;
- ausência de URLs ou credenciais da versão beta na configuração móvel.

As versões exatas devem ser registradas em cada release Android. Não utilizar versões presumidas.

---

## 4. Sincronização de correções

O Baluthi 2.0 é a origem funcional. Para cada correção ou pequeno lote:

1. concluir e validar a correção no Baluthi 2.0;
2. registrar o commit de origem;
3. replicar somente as mudanças necessárias para a cópia Android;
4. revisar conflitos e preservar as configurações móveis específicas;
5. aplicar migrations ou RPCs separadamente no backend Android;
6. validar que nenhuma configuração beta foi transportada;
7. executar o build e os testes Android;
8. registrar os commits e resultados na release.

Não substituir a cópia Android inteira ao final de um grande conjunto de mudanças, salvo decisão técnica formal. Não editar manualmente a mesma regra em dois lugares sem identificar a origem da alteração.

---

## 5. Validação do repositório

Antes do build:

1. confirmar branch e commit da cópia Android;
2. registrar o commit correspondente do Baluthi 2.0;
3. revisar o `package.json`;
4. confirmar a existência dos scripts móveis e dependências necessárias;
5. confirmar a pasta do projeto Android;
6. verificar se arquivos locais não versionados alteram o resultado;
7. confirmar a URL e o backend móvel;
8. pesquisar por referências ao ambiente beta ou produção;
9. confirmar que as migrations necessárias foram aplicadas somente no ambiente Android de teste.

Se o script móvel não estiver presente no `package.json`, o processo deve ser interrompido e a documentação/repositório reconciliados antes de continuar.

Se qualquer configuração apontar para o ambiente beta, o build não pode ser distribuído.

---

## 6. Sequência padrão

Executar, conforme os scripts realmente disponíveis no repositório:

```bash
bun install
bun run typecheck
bun run test
bun run build
```

Em seguida, executar o script móvel oficial da versão. Exemplo somente quando existente:

```bash
bun run mobile:build
```

Depois, sincronizar a camada web com o projeto Android usando o comando Capacitor configurado pelo projeto, por exemplo:

```bash
npx cap sync android
npx cap open android
```

Os comandos devem ser ajustados à configuração verificada do repositório. Não criar comandos paralelos sem registrar a mudança.

---

## 7. Android Studio

No Android Studio:

1. aguardar a sincronização do Gradle;
2. corrigir dependências somente após identificar a causa;
3. selecionar o módulo de aplicação;
4. escolher dispositivo físico ou emulador;
5. executar o app para teste local;
6. validar visualmente que o aplicativo abriu o ambiente móvel correto;
7. para gerar APK, utilizar a opção de build de APK disponível na versão instalada do Android Studio;
8. registrar o caminho exibido pelo Android Studio para o arquivo gerado.

A interface do Android Studio pode variar por versão. Quando a opção não estiver visível, pesquisar por “APK” ou usar o menu de geração de artefatos da versão instalada.

---

## 8. Artefatos

Para cada APK, registrar:

- nome do arquivo;
- versão do app;
- número do build;
- data e hora;
- commit da cópia Android;
- commit de origem do Baluthi 2.0;
- tipo de build;
- URL do ambiente móvel;
- identificação do backend Android;
- dispositivo(s) testado(s);
- hash do arquivo, quando aplicável;
- correções sincronizadas;
- problemas conhecidos.

Não usar nomes genéricos que impeçam identificar a versão.

---

## 9. Checklist de ambiente

Antes da instalação e distribuição, confirmar por escrito:

- [ ] URL móvel isolada;
- [ ] banco de dados Android separado;
- [ ] autenticação Android separada;
- [ ] armazenamento Android separado;
- [ ] funções e RPCs implantadas no ambiente Android;
- [ ] credenciais móveis próprias;
- [ ] URLs de redirecionamento próprias;
- [ ] e-mails transacionais de teste identificados;
- [ ] ausência de usuários ou dados da versão beta;
- [ ] uso exclusivo de dados fictícios.

Na dúvida, interromper o processo. Não tratar o APK como seguro até a confirmação técnica.

---

## 10. Solução de problemas

### Build web concluído, mas arquivos não aparecem no Android

- confirmar o diretório de saída usado pelo script móvel;
- confirmar a configuração `webDir` do Capacitor;
- executar novamente a sincronização do Capacitor;
- verificar se o Android Studio está aberto no projeto correto.

### Erro de Gradle ou JDK

- confirmar a versão de Java configurada no Android Studio;
- verificar a compatibilidade com Gradle e Android Gradle Plugin;
- evitar atualização isolada de Gradle sem documentar o impacto.

### Opção “Build APK” não localizada

- usar a busca de ações do Android Studio;
- pesquisar por “Build APK” ou “Generate APK”;
- observar que o nome e o menu mudam entre versões.

### App abre, mas utiliza ambiente beta ou incorreto

- interromper imediatamente os testes;
- desinstalar ou retirar o APK de circulação;
- revisar variáveis, URL, autenticação e configuração do build;
- não inserir dados nem executar migrations;
- registrar o incidente no documento da release;
- gerar um novo build somente após validação do isolamento.

### Correção funciona na web, mas não no Android

- confirmar se o commit foi sincronizado;
- revisar diferenças específicas do projeto móvel;
- confirmar se a migration ou RPC foi aplicada no backend Android;
- não apontar temporariamente o Android para o banco beta como atalho.

---

## 11. Critério de conclusão

O build Android só é considerado concluído quando:

- typecheck e testes obrigatórios foram executados;
- o APK foi gerado a partir de commits identificados;
- o ambiente Android isolado está documentado e validado;
- a instalação foi validada em dispositivo;
- os testes mínimos foram registrados;
- não há segredo ou chave de assinatura versionada;
- não há conexão com banco, autenticação ou armazenamento da versão beta;
- a documentação da release foi atualizada.
