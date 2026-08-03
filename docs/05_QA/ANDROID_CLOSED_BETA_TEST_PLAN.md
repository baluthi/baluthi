# Plano de testes Android — Closed Beta

**Status:** Obrigatório antes de distribuir APK  
**Data:** 2026-08-03

---

## 1. Objetivo

Validar que o aplicativo Android preserva as regras, segurança e experiência essenciais da versão web sem introduzir regressões específicas do ambiente móvel e sem acessar ou misturar dados da versão beta.

O ambiente Android deve utilizar banco de dados, autenticação, backend, armazenamento, credenciais, usuários e dados próprios.

---

## 2. Identificação do build

Registrar antes dos testes:

- versão e número do build;
- commit da cópia Android;
- commit correspondente do Baluthi 2.0;
- modelo do dispositivo;
- versão do Android;
- URL móvel utilizada;
- identificação do backend e banco Android;
- tipo de conexão utilizada;
- responsável pelo teste.

---

## 3. Pré-condições obrigatórias

Antes de qualquer teste funcional:

- [ ] confirmar que o APK aponta para `https://baluthi-mobile-poc.lovable.app` ou para outra URL móvel formalmente aprovada;
- [ ] confirmar banco Android separado da versão beta;
- [ ] confirmar autenticação Android separada;
- [ ] confirmar armazenamento Android separado;
- [ ] confirmar funções e RPCs no backend Android;
- [ ] confirmar credenciais e URLs de redirecionamento próprias;
- [ ] confirmar ausência de usuários, sessões e dados da versão beta;
- [ ] utilizar somente contas e dados fictícios.

Se qualquer item estiver inconclusivo, os testes devem ser interrompidos.

---

## 4. Testes mínimos

### Instalação e inicialização

- instalar e abrir o APK;
- validar ícone, nome, splash e primeira carga;
- confirmar ausência de tela branca ou erro de rede;
- confirmar visualmente o ambiente móvel correto;
- reabrir após encerrar o aplicativo.

### Isolamento entre beta e Android

- criar uma conta fictícia no Android e confirmar que ela não existe na versão beta;
- criar conta, cartão, categoria, lançamento, transferência e anexo no Android e confirmar que nenhum registro aparece na beta;
- confirmar que usuários da beta não autenticam automaticamente no Android;
- confirmar que sessões da beta não são reutilizadas;
- confirmar que anexos Android não aparecem no armazenamento beta;
- revisar logs e requisições para assegurar que URLs beta não são chamadas;
- confirmar que migrations e RPCs necessárias foram aplicadas no ambiente Android, não na beta.

Qualquer comunicação com o ambiente beta é falha bloqueadora.

### Autenticação

- criar conta fictícia de teste;
- entrar e sair;
- validar persistência de sessão;
- recuperar senha no ambiente Android;
- testar token inválido ou expirado;
- confirmar isolamento entre duas contas Android.

### Navegação móvel

- testar menu inferior e menu “Mais”;
- testar botão voltar do Android;
- abrir e fechar modais;
- alternar entre app e outro aplicativo;
- testar rotação, quando suportada;
- confirmar que o painel administrativo não está disponível no aplicativo móvel.

### Formulários e teclado

- cadastrar e editar contas, cartões, categorias e recorrências;
- registrar receita, despesa e transferência;
- verificar máscaras monetárias;
- confirmar que o teclado não oculta botões críticos;
- validar datas, seletores e rolagem.

### Regras financeiras

- transferência deve afetar as duas contas;
- cancelamento/estorno de transferência deve reverter os dois lados;
- compra no cartão deve entrar na fatura correta;
- cancelamento de compra deve preservar histórico e retirar impacto financeiro;
- contas vazias podem seguir o fluxo aprovado de exclusão;
- contas com histórico devem respeitar arquivamento e bloqueios.

### Sincronização de correções

Para cada lote vindo do Baluthi 2.0:

- registrar o commit de origem;
- confirmar que os arquivos corretos foram replicados;
- confirmar que configurações móveis específicas foram preservadas;
- validar a correção no Android;
- confirmar que eventual migration/RPC foi aplicada separadamente no backend Android;
- executar regressão do fluxo relacionado;
- registrar qualquer divergência entre web e Android.

### Anexos e permissões

- testar câmera, galeria e PDF separadamente;
- confirmar solicitação de permissão apenas no momento necessário;
- cancelar o seletor sem travar o formulário;
- validar anexos após reabrir o lançamento;
- testar isolamento de anexos entre usuários Android;
- confirmar que os arquivos não são gravados no armazenamento beta.

### Rede e resiliência

- testar Wi‑Fi e rede móvel;
- interromper a conexão durante uma operação;
- impedir duplicidade após nova tentativa;
- validar mensagens compreensíveis;
- reabrir após falha de rede.

### Relatórios

- gerar relatórios com filtros;
- validar visualização móvel;
- validar somente a tela de geração quando o PDF não estiver adequado ao formato móvel;
- gerar PDF quando fizer parte do build testado;
- confirmar logo, layout e conteúdo;
- testar compartilhamento ou abertura do arquivo, quando suportado.

### Privacidade e segurança

- confirmar que e-mails e dados pessoais não aparecem indevidamente;
- testar acesso cruzado com duas contas Android;
- tentar alterar IDs em requisições, quando possível;
- validar que usuário comum não acessa funções administrativas;
- confirmar ausência de segredos nos logs e no APK;
- confirmar ausência de URLs, chaves ou identificadores do ambiente beta.

---

## 5. Compatibilidade mínima

Testar, sempre que houver disponibilidade:

- ao menos um aparelho físico Samsung ou equivalente;
- tela pequena e tela grande;
- versão Android mais antiga ainda suportada;
- versão Android recente;
- conexão lenta ou instável.

A matriz real deve ser registrada na release.

---

## 6. Severidade

- **Bloqueador:** conexão com ambiente beta, mistura ou exposição de dados, perda de dados, acesso indevido, falha de autenticação, saldo incorreto ou app não inicia.
- **Alta:** fluxo financeiro crítico não conclui ou fica inconsistente.
- **Média:** funcionalidade funciona com dificuldade ou mensagem inadequada.
- **Baixa:** problema visual sem impacto funcional relevante.

Nenhum bloqueador ou alta gravidade pode permanecer aberto na distribuição do APK sem decisão formal registrada.

---

## 7. Evidências

Para cada falha, registrar:

- passos de reprodução;
- resultado esperado e observado;
- captura de tela ou vídeo;
- dispositivo e Android;
- versão e commits;
- ambiente afetado;
- logs úteis sem dados sensíveis;
- decisão e correção aplicada.

---

## 8. Aprovação

O APK somente pode ser encaminhado aos testadores quando:

- o ambiente Android isolado estiver identificado e validado;
- os fluxos críticos forem aprovados;
- não houver comunicação com banco, autenticação ou armazenamento da versão beta;
- não houver falha de segurança ou integridade conhecida;
- os problemas restantes estiverem documentados;
- o registro da release estiver atualizado.
