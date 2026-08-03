# Guia de build Android — Baluthi

**Status:** Ativo para testes do Closed Beta  
**Data:** 2026-08-03

---

## 1. Objetivo

Padronizar a geração do aplicativo Android de teste da Baluthi, evitando divergências entre máquinas, builds e ambientes.

Este guia não autoriza publicação na Play Store. O artefato atual é destinado a testes controlados.

---

## 2. Pré-requisitos

Antes de iniciar, confirmar:

- acesso ao repositório oficial da aplicação;
- Node.js e gerenciador de pacotes compatíveis com o projeto;
- Java/JDK compatível com a versão do Android Gradle Plugin;
- Android Studio atualizado e SDK Android instalado;
- dispositivo físico ou emulador disponível;
- variáveis de ambiente corretas para o ambiente de teste;
- ausência de chaves, senhas ou arquivos de assinatura no Git.

As versões exatas devem ser registradas em cada release Android. Não utilizar versões presumidas.

---

## 3. Validação do repositório

Antes do build:

1. confirmar branch e commit;
2. revisar o `package.json`;
3. confirmar a existência dos scripts móveis e dependências necessárias;
4. confirmar a pasta do projeto Android;
5. verificar se arquivos locais não versionados alteram o resultado;
6. registrar o backend e as URLs que serão utilizados pelo APK.

Se o script móvel não estiver presente no `package.json`, o processo deve ser interrompido e a documentação/repositório reconciliados antes de continuar.

---

## 4. Sequência padrão

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

Os comandos acima devem ser ajustados à configuração verificada do repositório. Não criar comandos paralelos sem registrar a mudança.

---

## 5. Android Studio

No Android Studio:

1. aguardar a sincronização do Gradle;
2. corrigir dependências somente após identificar a causa;
3. selecionar o módulo de aplicação;
4. escolher dispositivo físico ou emulador;
5. executar o app para teste local;
6. para gerar APK, utilizar a opção de build de APK disponível na versão instalada do Android Studio;
7. registrar o caminho exibido pelo Android Studio para o arquivo gerado.

A interface do Android Studio pode variar por versão. Quando a opção não estiver visível, pesquisar por “APK” ou usar o menu de geração de artefatos da versão instalada.

---

## 6. Artefatos

Para cada APK, registrar:

- nome do arquivo;
- versão do app;
- número do build;
- data e hora;
- commit de origem;
- tipo de build;
- ambiente de backend;
- dispositivo(s) testado(s);
- hash do arquivo, quando aplicável;
- problemas conhecidos.

Não usar nomes genéricos que impeçam identificar a versão.

---

## 7. Dados e ambientes

Antes da instalação, confirmar por escrito:

- se o APK acessa produção, homologação ou outro ambiente;
- qual banco de dados é utilizado;
- qual serviço de autenticação é utilizado;
- onde os comprovantes são armazenados;
- quais URLs de redirecionamento estão liberadas;
- se e-mails transacionais podem ser enviados por testes.

Na dúvida, tratar o APK como conectado ao ambiente de produção e não utilizar dados sensíveis até a confirmação.

---

## 8. Solução de problemas

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

### App abre, mas utiliza ambiente incorreto

- interromper os testes;
- revisar variáveis e configuração do build;
- não corrigir manualmente apenas no projeto nativo sem reconciliar o código-fonte;
- registrar o incidente no documento da release.

---

## 9. Critério de conclusão

O build Android só é considerado concluído quando:

- typecheck e testes obrigatórios foram executados;
- o APK foi gerado a partir de commit identificado;
- o ambiente utilizado está documentado;
- a instalação foi validada em dispositivo;
- os testes mínimos foram registrados;
- não há segredo ou chave de assinatura versionada;
- a documentação da release foi atualizada.
