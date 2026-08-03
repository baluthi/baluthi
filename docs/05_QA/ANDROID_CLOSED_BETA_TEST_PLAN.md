# Plano de testes Android — Closed Beta

**Status:** Obrigatório antes de distribuir APK  
**Data:** 2026-08-03

---

## 1. Objetivo

Validar que o aplicativo Android preserva as regras, segurança e experiência essenciais da versão web, sem introduzir regressões específicas do ambiente móvel.

---

## 2. Identificação do build

Registrar antes dos testes:

- versão e número do build;
- commit de origem;
- modelo do dispositivo;
- versão do Android;
- ambiente de backend;
- tipo de conexão utilizada;
- responsável pelo teste.

---

## 3. Testes mínimos

### Instalação e inicialização

- instalar e abrir o APK;
- validar ícone, nome, splash e primeira carga;
- confirmar ausência de tela branca ou erro de rede;
- reabrir após encerrar o aplicativo.

### Autenticação

- criar conta de teste;
- entrar e sair;
- validar persistência de sessão;
- recuperar senha;
- testar token inválido ou expirado;
- confirmar isolamento entre duas contas.

### Navegação móvel

- testar menu inferior e menu “Mais”;
- testar botão voltar do Android;
- abrir e fechar modais;
- alternar entre app e outro aplicativo;
- testar rotação, quando suportada.

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

### Anexos e permissões

- testar câmera, galeria e PDF separadamente;
- confirmar solicitação de permissão apenas no momento necessário;
- cancelar o seletor sem travar o formulário;
- validar anexos após reabrir o lançamento;
- testar isolamento de anexos entre usuários.

### Rede e resiliência

- testar Wi‑Fi e rede móvel;
- interromper a conexão durante uma operação;
- impedir duplicidade após nova tentativa;
- validar mensagens compreensíveis;
- reabrir após falha de rede.

### Relatórios

- gerar relatórios com filtros;
- validar visualização móvel;
- gerar PDF;
- confirmar logo, layout e conteúdo;
- testar compartilhamento ou abertura do arquivo, quando suportado.

### Privacidade e segurança

- confirmar que e-mails e dados pessoais não aparecem indevidamente;
- testar acesso cruzado com duas contas;
- tentar alterar IDs em requisições, quando possível;
- validar que usuário comum não acessa funções administrativas;
- confirmar ausência de segredos nos logs e no APK.

---

## 4. Compatibilidade mínima

Testar, sempre que houver disponibilidade:

- ao menos um aparelho físico Samsung ou equivalente;
- tela pequena e tela grande;
- versão Android mais antiga ainda suportada;
- versão Android recente;
- conexão lenta ou instável.

A matriz real deve ser registrada na release.

---

## 5. Severidade

- **Bloqueador:** perda de dados, acesso indevido, falha de autenticação, saldo incorreto, app não inicia.
- **Alta:** fluxo financeiro crítico não conclui ou fica inconsistente.
- **Média:** funcionalidade funciona com dificuldade ou mensagem inadequada.
- **Baixa:** problema visual sem impacto funcional relevante.

Nenhum bloqueador ou alta gravidade pode permanecer aberto na distribuição do Closed Beta sem decisão formal registrada.

---

## 6. Evidências

Para cada falha, registrar:

- passos de reprodução;
- resultado esperado e observado;
- captura de tela ou vídeo;
- dispositivo e Android;
- versão/commit;
- logs úteis sem dados sensíveis;
- decisão e correção aplicada.

---

## 7. Aprovação

O APK somente pode ser encaminhado aos testadores quando:

- o ambiente estiver identificado;
- os fluxos críticos forem aprovados;
- não houver falha de segurança ou integridade conhecida;
- os problemas restantes estiverem documentados;
- o registro da release estiver atualizado.
