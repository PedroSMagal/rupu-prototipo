<p align="center">
  <img src="assets/logo.png" alt="Logo do R.U.P.U. – Restaurante Universitário Para Universitários" width="560">
</p>

# R.U.P.U. – Restaurante Universitário Para Universitários

Protótipo navegável de um aplicativo para celular que reúne as informações do Restaurante Universitário (RU) da UESC. O projeto foi desenvolvido como trabalho da disciplina de **Interação Humano-Máquina (IHM)** e tem dois objetivos: resolver um problema real do campus e demonstrar, em uma interface concreta, os conceitos estudados em sala.

> **Status:** protótipo de alta fidelidade, sem backend. Todos os dados (cardápio, fila, fichas, usuários) são de exemplo e nada é salvo ao recarregar a página.

---

## Sumário

1. [Problema e público](#1-problema-e-público)
2. [Funcionalidades](#2-funcionalidades)
3. [Decisões de design](#3-decisões-de-design)
4. [Aplicação dos conceitos de IHM](#4-aplicação-dos-conceitos-de-ihm)
5. [Decisões por tela](#5-decisões-por-tela)
6. [Decisões de conteúdo e regras de negócio](#6-decisões-de-conteúdo-e-regras-de-negócio)
7. [Decisões técnicas](#7-decisões-técnicas)
8. [Como executar e testar](#8-como-executar-e-testar)
9. [Limitações conhecidas](#9-limitações-conhecidas)
10. [Próximos passos](#10-próximos-passos)
11. [Fontes e créditos](#11-fontes-e-créditos)

---

## 1. Problema e público

O RU da UESC não tem site nem aplicativo. Hoje, o aluno só descobre o cardápio, o tamanho da fila, se a comida acabou ou se o RU está fechado **depois de chegar ao local**. O pagamento funciona apenas com dinheiro físico.

**Público principal:** estudantes de graduação e pós-graduação, que usam o RU de forma recorrente, geralmente com pressa entre aulas e com o celular na mão.

Dessa realidade vieram três prioridades de projeto:

- **Responder rápido às perguntas mais comuns** ("está aberto?", "tem fila?", "ainda tem ficha?") logo na primeira tela.
- **Funcionar bem no celular**, em pé, com uma mão e com pouca atenção.
- **Reduzir o atrito de entrar no RU**, trocando dinheiro físico por saldo no app e QR code.

## 2. Funcionalidades

| Área | O que o app oferece |
|---|---|
| **Início** | Saudação com o primeiro nome, timer de abertura/fechamento, fichas restantes, nível de fila com tempo médio, atalho para o QR code e pesquisa de satisfação opcional |
| **Cardápio** | Hoje e próximos dias; café da manhã, almoço e jantar; opções vegetarianas e tradicionais; status de cada item (tem, acabando, acabou) |
| **Carteira** | Saldo, QR code de entrada com uso único por refeição, recarga por Pix ou cartão com confirmação e opção de desfazer |
| **Notícias** | Enquete de cardápio (com resultado após o voto e possibilidade de alterar) e comunicados |
| **Avisos** | Alertas de fechamento e manutenção, preferências de notificação, dados da conta e contato |
| **Conta** | Login por matrícula e senha, criação de conta só com matrícula e senha (nome e e-mail vêm da base da UESC), recuperação de senha pelo e-mail institucional |
| **Modo "Ver IHM"** | Botão no topo que marca cada elemento com o princípio de IHM que ele aplica |

## 3. Decisões de design

### 3.1 Cores

As cores vêm do **manual de identidade visual da Pró-Reitoria de Extensão (PROEX) da UESC**, que por sua vez se baseia no Brasão da universidade.

| Cor | Hex | Papel no app | Origem / justificativa |
|---|---|---|---|
| Azul | `#2259A6` | Cor principal: cabeçalho, menu ativo, seleções | Azul do Brasão ("entre o mar e o céu"); transmite confiança e institucionalidade |
| Laranja | `#FEA621` | Botões de ação principal, faixa sob o cabeçalho, nível da fila | Cor das "labaredas" do Brasão; é **complementar** do azul, o que cria o maior contraste de matiz possível e faz o botão principal se destacar |
| Vermelho | `#C2000B` | Somente erros, itens esgotados e RU fechado | Reservado para **estados negativos**: como não aparece em decoração, o alerta se destaca imediatamente |
| Preto / quase-preto | `#000000` / `#0D1320` | Texto sobre o laranja; texto geral | O preto do manual aparece no texto dos botões laranja, onde dá o maior contraste |

Cores de apoio (neutras e semânticas):

- Fundo `#F2F5FA`, cartões `#FFFFFF`, bordas `#C5D0E0`, texto secundário `#48556B`, azul claro `#DCE7F6`.
- Verde para "tem" (`#166534` sobre `#DCF2E3`) e âmbar para "acabando" (`#8A4B00` sobre `#FFEBC7`). O verde **não** faz parte da marca da UESC; foi mantido porque verde = "disponível" é uma convenção universal e o usuário precisa entender o status sem aprender nada novo.

**Regras de uso aplicadas**

- **Proporção 60-30-10:** ~60% neutros, ~30% azul, ~10% laranja e demais acentos.
- **Cor nunca é a única informação.** Todo status tem ícone e texto (✓ Tem, ! Acabando, ✕ Acabou), o que atende pessoas com daltonismo.
- **Cada cor tem um significado fixo.** Laranja = "toque aqui"; vermelho = "problema"; azul = "estrutura e marca".
- **Contraste:** pares de texto/fundo foram escolhidos para atingir o nível AA da WCAG (4,5:1 para texto comum). Os valores foram estimados no projeto e vale confirmar com uma ferramenta de contraste antes da versão final.

### 3.2 Logo

O logo do R.U.P.U. (arquivo `assets/logo.png`) mostra um prato com garfo e faca sob um capelo de formatura, com uma curva laranja ao redor. A leitura é direta: **comida + universidade**. As cores do logo (azul em torno de `#014293` e laranja em torno de `#FF9608`) são próximas às da paleta do app, então a marca e a interface parecem uma coisa só.

Como o logo foi usado no app:

- **Telas de entrada (login, cadastro e recuperação de senha):** logo completo no topo, dentro de um **cartão branco**. O logo tem fundo transparente e letras azul-escuras, que perderiam contraste no modo escuro; o cartão branco garante a leitura nos dois temas.
- **Cabeçalho:** somente o **emblema** (prato + capelo), em um quadrado branco de 46 px ao lado do nome. O logo completo ficaria pequeno demais no celular, e o emblema funciona como ícone de reconhecimento rápido.
- **Peso da imagem:** as imagens foram reduzidas (logo em 720 px de largura e emblema em 160 px) e convertidas para WebP, ficando em ~40 KB e ~12 KB, embutidas no próprio HTML. Assim o app continua sendo um arquivo único e abre rápido.

### 3.3 Modo escuro

O app segue a preferência do sistema (`prefers-color-scheme`). No escuro, o azul vira uma versão mais clara (`#7FB0F2`) para manter o contraste sobre o fundo `#0B1220`, e o laranja permanece igual, porque já tem bom contraste nos dois temas. O modo escuro ajuda quem usa o app à noite (jantar) e reduz o cansaço visual.

### 3.4 Tipografia

- **Atkinson Hyperlegible** (Google Fonts), com fallback para a fonte do sistema.
- Foi desenhada pelo Braille Institute para **maximizar a distinção entre caracteres parecidos** (como I, l, 1 e O, 0), o que beneficia pessoas com baixa visão e, na prática, todos que leem no celular sob sol ou com pressa.
- Texto de corpo em 16 px, secundário em 14 px (nunca menor que 12 px) e números grandes em 34 px para os dados que o usuário quer ver "de relance" (timer, fichas, saldo).
- Números com `tabular-nums`, para que o timer não "pule" a cada segundo.

### 3.5 Layout e navegação

- **Barra de navegação inferior com 5 abas** (Início, Cardápio, Carteira, Notícias, Avisos). No celular, a parte de baixo da tela é a zona alcançada com mais facilidade pelo polegar.
- **Aba ativa com três sinais:** cor, peso da fonte e uma barra no topo do botão. Assim, a localização do usuário não depende só da cor.
- **Cartões** agrupam informações relacionadas (lei da proximidade da Gestalt): estado do RU, fichas e fila ficam em blocos separados.
- **Hierarquia visual:** o dado mais importante de cada cartão é o maior; a explicação fica em texto secundário.
- **Moldura de celular no computador.** Em telas largas, o app é exibido em uma moldura de 390 px, o que dá noção de como será no aparelho.

### 3.6 Ergonomia

- **Alvos de toque de pelo menos 44 px** (botões, chips, itens de lista, aba do menu com 60 px), seguindo as recomendações de Apple e WCAG para reduzir erros de toque.
- **Ação principal sempre larga** (largura total, 48 px de altura) e na cor de destaque.
- **Ações de risco ficam longe do polegar por padrão e pedem confirmação.**
- **Respeito a áreas seguras** (`safe-area-inset`) para não colar conteúdo em notch ou barra do sistema.

## 4. Aplicação dos conceitos de IHM

### 4.1 As 8 Regras de Ouro de Shneiderman

| # | Regra | Como aparece no app |
|---|---|---|
| 1 | Buscar consistência | Mesmos componentes para escolhas únicas (controle segmentado no filtro e no pagamento), mesma cor para ações e mesmos nomes para a mesma ação ("Confirmar", "Cancelar", "Desfazer") |
| 2 | Atalhos para usuários frequentes | Botão "Mostrar meu QR code" direto no Início, para quem entra todo dia; o login lembra o formato da matrícula e aceita Enter para entrar |
| 3 | Feedback informativo | Toast após recarga, aviso de leitura do QR, mensagem após enviar avaliação, contador de itens do filtro |
| 4 | Diálogos com fechamento | A recarga tem início (escolher valor), meio (confirmar) e fim (aviso "Saldo adicionado"); o cadastro termina com a entrada no app |
| 5 | Prevenção de erros e tratamento simples | Confirmação antes de pagar, validação do cadastro (matrícula de 9 dígitos que precisa existir na base, senha mínima) com mensagens que dizem como corrigir |
| 6 | Reversão fácil de ações | Botão "Desfazer" por 6 segundos após recarga; "Alterar meu voto" na enquete; "Cancelar" na avaliação; "Reiniciar demonstração" |
| 7 | Locus de controle interno | Pesquisa de satisfação opcional ("Agora não"), notificações configuráveis, filtros que o usuário liga e desliga; o app nunca bloqueia o fluxo principal |
| 8 | Reduzir carga de memória de curto prazo | Reconhecer em vez de lembrar: o QR substitui senha/ficha, o cardápio mostra o status ao lado de cada item, o filtro exibe contagens e a recarga repete o valor na confirmação |

### 4.2 As 10 Heurísticas de Nielsen

| # | Heurística | Onde está |
|---|---|---|
| 1 | Visibilidade do estado do sistema | Timer, badge "Aberto/Fechado", fichas restantes, nível de fila, status dos itens, estado do QR ("1 uso disponível" ou "Já usado") |
| 2 | Correspondência com o mundo real | Linguagem do aluno ("fichas", "fila", "catraca", "almoço"), saudação pelo primeiro nome, ícones de comida |
| 3 | Controle e liberdade do usuário | Desfazer, cancelar, voltar, mostrar/ocultar senha |
| 4 | Consistência e padrões | Mesmos padrões visuais e de texto em todas as abas; convenções de cor (verde/âmbar/vermelho) |
| 5 | Prevenção de erros | Confirmação de pagamento, campo de matrícula só numérico, limite de caracteres, validações antes de enviar |
| 6 | Reconhecer em vez de lembrar | Filtros com ícones e contagem, "Dados de teste" visíveis no login, horários sempre exibidos ao lado do timer |
| 7 | Flexibilidade e eficiência de uso | Atalho para o QR, filtros por dieta, tecla Enter no login |
| 8 | Design estético e minimalista | Poucas cores, um destaque por tela, sem decoração que não informe |
| 9 | Ajudar a reconhecer, diagnosticar e corrigir erros | Mensagens em linguagem simples, sem códigos ("Matrícula ou senha incorreta. Confira os dados ou toque em 'Esqueci a senha'") |
| 10 | Ajuda e documentação | Aba Avisos com contato, textos de apoio sob os campos, botão "Ver IHM" explicando as decisões |

### 4.3 Outros conceitos de IHM usados

- **Gestalt:** proximidade (cartões), semelhança (todos os botões de ação têm a mesma forma e cor), continuidade (listas alinhadas) e figura/fundo (cartões brancos sobre fundo azul-acinzentado).
- **Lei de Fitts:** alvos grandes e botões principais na parte inferior, reduzindo tempo e erro de toque.
- **Lei de Hick:** poucas opções por tela (5 abas, 3 refeições, 3 filtros, 3 valores de recarga), o que acelera a decisão.
- **Carga cognitiva:** informação dividida em pequenos blocos; o dado importante é o maior de cada bloco.
- **Acessibilidade (WCAG):** contraste, status com texto e ícone, foco visível em azul `#2563EB`, `aria-label`/`role` em controles personalizados (`radiogroup`, `switch`, `tab`, `dialog`), `aria-live` e `role="status"` para mensagens, respeito a `prefers-reduced-motion`.

## 5. Decisões por tela

### 5.1 Login, cadastro e recuperação de senha

- **Login por matrícula**, porque é o identificador que o aluno já conhece de cor e que liga a pessoa ao vínculo com a universidade.
- **Cadastro com apenas dois campos: matrícula e senha.** O app busca nome e e-mail institucional na base da UESC a partir da matrícula, o que reduz o esforço de digitação (menos campos, menos erros) e evita dados inconsistentes.
- **Feedback imediato:** ao digitar uma matrícula existente, o app mostra "✓ Encontramos: Maria" (só o primeiro nome, para expor o mínimo de dados pessoais) e o usuário confirma que é ele mesmo.
- **Sem campo de repetir senha.** Em vez disso, o botão "Mostrar senha" permite conferir o que foi digitado, o que dá o mesmo efeito de prevenção de erro com um campo a menos.
- **Mensagens de erro juntas e claras:** matrícula com 9 números, matrícula inexistente na base, matrícula que já tem conta e senha com menos de 6 caracteres.
- **Recuperação pelo e-mail institucional.** O app mostra o e-mail **mascarado** (`phs***@uesc.br`): confirma ao usuário para onde foi sem expor o endereço inteiro.
- **"Mostrar senha"** como botão explícito, o que reduz erros de digitação no celular sem forçar o usuário a repetir a senha no login.
- **Primeiro nome na saudação** ("Olá, Pedro!"): personaliza sem expor o nome completo na tela principal.

### 5.2 Início

- **Ordem dos cartões = ordem das perguntas do aluno:** 1) Está aberto? 2) Ainda tem ficha? 3) Como está a fila? 4) Quero entrar.
- **Timer com dois estados:** "Fecha em" quando aberto e "Abre em" quando fechado, sempre com o horário da refeição logo abaixo.
- **Fichas com barra de progresso e número grande**, mais selo "Restam poucas" em âmbar. O alerta combina texto, ícone e cor.
- **Fila em 3 níveis** (barra segmentada) mais tempo médio em minutos, mais uma dica de horário melhor.
- **Pesquisa de satisfação opcional:** a nota abre etiquetas rápidas (Sabor, Temperatura, Quantidade, Fila, Limpeza) e um campo de texto "Por que essa nota?". As etiquetas reduzem o esforço de quem tem pressa e o texto livre dá contexto a quem quiser escrever. Pode ser dispensada com "Agora não".

### 5.3 Cardápio

- **Dias e refeições como abas** com rótulo e data, para o usuário saber sempre onde está.
- **Dias futuros mostram "Cardápio previsto"**, sem status de disponibilidade (que só faz sentido no dia).
- **Feriado tratado como estado explícito:** a sexta (20/11) mostra "RU fechado" em vez de uma lista vazia.
- **Filtro redesenhado.** A primeira versão usava botões pequenos e soltos. A versão final é um **controle segmentado** com:
  - ícone + nome + quantidade de itens (reconhecer em vez de lembrar);
  - a opção ativa totalmente preenchida (estado visível);
  - uma linha de resumo abaixo ("6 itens para vegetarianos. Itens sem etiqueta servem a todos");
  - botões grandes de 58 px, com seleção única, no mesmo padrão da forma de pagamento (consistência).
- **Itens esgotados ficam riscados e com selo vermelho**, o que dá três pistas redundantes (texto, ícone, estilo).

### 5.4 Carteira

- **Saldo em destaque** e **preço da refeição (R$ 1,00)** logo abaixo.
- **QR code mostra para qual refeição vale** e seu estado (✓ 1 uso disponível / ✕ Já usado).
- **Uso único por refeição:** depois de lido, o QR fica cinza com explicação ("Um novo QR vale na próxima refeição"). Isso previne fraude (print compartilhado) e comunica a regra no próprio lugar onde ela se aplica.
- **Recarga em 3 passos:** forma de pagamento (Pix ou cartão), valor (R$ 10, 20 ou 50) e confirmação. A confirmação repete valor, forma e saldo final.
- **"Desfazer" por 6 segundos** depois de confirmar, porque erros de toque são comuns no celular.
- **Botões de simulação** ("Simular leitura na catraca", "Reiniciar demonstração") existem só para testar o protótipo e estão rotulados como tal.

### 5.5 Notícias e Avisos

- **Enquete:** voto único, resultado em barras logo após votar (feedback imediato) e opção de alterar o voto.
- **Comunicados** curtos, com título claro. O aviso do Circuito das Profissões informa que o RU fechará mais tarde, sem prometer horários que ainda não foram definidos.
- **Avisos separados por gravidade:** vermelho para fechamento, âmbar para aviso informativo. O ícone de sino no menu tem um contador.
- **Notificações configuráveis** com interruptores grandes (fichas acabando, abertura, fila baixa, fechamento).

## 6. Decisões de conteúdo e regras de negócio

| Decisão | Valor | Motivo |
|---|---|---|
| Preço da refeição | R$ 1,00 | Definido pelo autor do projeto |
| Café da manhã | 7h–9h | Definido pelo autor |
| Almoço | 11h–14h | Definido pelo autor |
| Jantar | 18h–20h | Definido pelo autor |
| Dias de funcionamento | Dias úteis | O RU abre segunda a sexta; o timer pula sábado e domingo |
| Feriado | 20/11/2026 fechado | Consciência Negra; mostra como o app comunica exceções |
| Sobremesa | Não há | O RU não serve sobremesa; foi removida do cardápio |
| Opção vegetariana | Item próprio e etiquetado | Em vez de esconder, o app indica quando há proteína vegetal |
| Uso do QR | 1 leitura por refeição | Evita fraude e compartilhamento |
| Cobrança | Débito de R$ 1,00 no saldo ao ler o QR | Simula a entrada na catraca |

## 7. Decisões técnicas

- **Um único arquivo HTML**, com CSS e JavaScript embutidos, sem framework e sem dependências além da fonte do Google Fonts. Facilita abrir, compartilhar e entregar.
- **JavaScript puro:** simples de ler e explicar em sala. O estado fica em variáveis em memória.
- **Variáveis CSS** para todas as cores e dois conjuntos (claro e escuro), o que permite trocar a identidade visual alterando poucas linhas.
- **QR code ilustrativo.** O desenho é gerado por um padrão pseudoaleatório com os três marcadores de canto; **não é um QR legível** por leitor real.
- **Timer baseado no relógio real** do dispositivo, aplicando os horários e o feriado cadastrados.
- **Autenticação simulada.** Os usuários ficam em memória e a senha é comparada em texto simples. Isso é aceitável só em um protótipo.
- **Layout responsivo:** ocupa a tela toda no celular e usa moldura de 390 px em telas largas.

## 8. Como executar e testar

**Abrir:** abra o link do protótipo publicado ou o arquivo `.html` no navegador (celular ou computador).

**Dados de teste**

| Campo | Valor |
|---|---|
| Matrícula | `202410129` |
| Senha | `123456` |
| Nome | Pedro Henrique Soares Magalhães |
| E-mail | `phsmagalhaes.cic@uesc.br` |

Para testar **Criar conta**, use uma destas matrículas ainda sem conta: `202410130`, `202320045` ou `202510077` (a `202410129` já tem conta).

**Roteiro sugerido**

1. Entre com os dados de teste e confira o "Olá, Pedro!".
2. No Início, leia o estado do RU, as fichas e a fila. Para ver "Aberto" e "Fechado", teste dentro e fora dos horários.
3. No Cardápio, navegue pelos dias e refeições e use o filtro. Abra a sexta (20/11).
4. Na Carteira, escolha Pix ou cartão, adicione R$ 20 e use **Desfazer**.
5. Toque em **Simular leitura na catraca** duas vezes: a segunda deve ser recusada.
6. Em Notícias, vote na enquete e altere o voto.
7. No Início, avalie o almoço com nota, etiquetas e texto.
8. Saia da conta e teste **Criar conta** (só matrícula e senha) e **Esqueci a senha**.
9. Toque em **Ver IHM** e confira os princípios em cada tela.

**Testes de usabilidade sugeridos**

- Peça a 3 a 5 colegas tarefas como "descubra se ainda tem fila agora" ou "recarregue R$ 20 e mostre o QR", **sem explicar nada**. Anote hesitações, erros e tempo.
- Teste no modo escuro, com fonte grande e navegando só com a tecla `Tab`.
- Confira se "Tem", "Acabando" e "Acabou" são compreensíveis sem cor.

## 9. Limitações conhecidas

- Não há backend: nada é salvo, enviado ou sincronizado; e-mail de recuperação, Pix e cartão são apenas telas.
- O QR code não é real e não pode ser lido por leitores.
- Fila, fichas, cardápio, notícias e votos são dados fixos de exemplo.
- A "base da UESC" é simulada: apenas 4 matrículas de exemplo existem. Na versão real, a matrícula sozinha **não prova quem a pessoa é** (qualquer um poderia criar conta com a matrícula de outro aluno). Será preciso confirmar a identidade, por exemplo com um código enviado ao e-mail institucional.
- A senha em texto simples e a caixa "Dados de teste" no login **não podem existir numa versão real**.
- Cardápio, horários e feriado estão cadastrados apenas para novembro de 2026.
- Os contrastes de cor foram estimados, não medidos por ferramenta.
- O app não foi testado com leitores de tela reais nem com usuários reais; os testes sugeridos acima são o próximo passo.

## 10. Próximos passos

- Backend com autenticação segura (senha com hash, recuperação por link com prazo, sessão) e integração com a base de alunos da UESC para o cadastro por matrícula, com verificação por código no e-mail institucional.
- Integração com o sistema do RU para fichas, fila e cardápio em tempo real.
- Pagamento por Pix e cartão com gateway real e comprovante.
- QR code dinâmico e de curta duração, validado na catraca.
- Notificações push para abertura, fichas e fila.
- Medição de contraste e teste com leitores de tela.
- Testes de usabilidade com alunos e ajustes a partir dos resultados.
- Versão para computador, com a mesma identidade visual.

## 11. Fontes e créditos

- Cores: *Identidade Visual da Pró-Reitoria de Extensão da UESC (PROEX)*, que se baseia no Brasão da UESC. Cores usadas: `#2259A6`, `#FEA621`, `#C2000B` e preto.
- Princípios: Ben Shneiderman, *Oito Regras de Ouro do Design de Interfaces*; Jakob Nielsen, *10 Heurísticas de Usabilidade*.
- Diretrizes de acessibilidade: WCAG 2.x (W3C).
- Fonte: *Atkinson Hyperlegible*, do Braille Institute.
- Logo do R.U.P.U.: criado para este projeto (`assets/logo.png`).
- Projeto acadêmico da disciplina de Interação Humano-Máquina. Nome, marca e dados da UESC pertencem à instituição; este protótipo não é um produto oficial.
