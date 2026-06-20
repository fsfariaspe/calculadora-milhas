# Calculadora de Passagens Viaje Fácil Brasil: Emissões (Milhas vs. Dinheiro)

A **Calculadora de Passagens Viaje Fácil Brasil** é um utilitário web de alta performance desenvolvido para otimizar e automatizar a comparação financeira de emissões de passagens aéreas. O sistema ajuda a responder de forma instantânea a pergunta clássica de todo milheiro e consultor de viagens: **vale a pena emitir com milhas puras, milhas + dinheiro (coparticipação) ou pagar a passagem 100% em dinheiro?**

O grande diferencial da ferramenta é a automação da entrada de dados por meio de **Reconhecimento Óptico de Caracteres (OCR) executado diretamente no navegador do cliente (client-side)**, eliminando a digitação manual de múltiplos valores de pontos e taxas de embarque.

---

## ✨ Principais Funcionalidades

*   **Importação por Print (OCR Local)**: Copie a tela de busca da sua companhia aérea e cole diretamente na ferramenta com `Ctrl+V` (ou clique para enviar a imagem). O processamento ocorre 100% no seu computador, de forma segura e instantânea.
*   **Algoritmo de Pareamento por Proximidade**: Resolve problemas comuns de OCR (como desalinhamento de colunas de texto) associando inteligentemente cada bloco de milhas com a coparticipação correspondente da mesma opção de forma espacial.
*   **Heurística Corretiva de Proporção (Smiles 30% Ratio)**: Em emissões de milhas + dinheiro (modalidade mista), companhias aéreas como a Smiles utilizam proporções matemáticas exatas da tarifa base (geralmente exigindo exatamente 30% da milhagem cheia). Por limitações do OCR ao analisar imagens comprimidas, o dígito inicial `9` (ex: `9.570 milhas`) costuma ser erroneamente interpretado como `2` (lido como `2.570 milhas`). O algoritmo detecta essa falha recalculando a proporção exata da tarifa de 100% milhas e corrige automaticamente a leitura do dígito inicial.
*   **Camada de Tolerância Óptica (LATAM Pass)**: Normaliza decimais, remove espaços adicionados incorretamente e trata prefixos colados de moedas (`BRL140` $\rightarrow$ `r$ 140`).
*   **Comparativo de Custo Total Equivalente**: Calcula o custo financeiro real de todas as opções de pontos sob o valor de mercado (ou de custo) do seu milheiro de referência.
*   **Integração com 100% Dinheiro**: Permite inserir o preço em dinheiro da passagem, gerando o **Milheiro Equivalente da Passagem** para decidir se vale a pena guardar as milhas para outra viagem.
*   **Visualização Clara**: Gráfico de barras dinâmico de custos equivalentes com indicação de economia e detalhamento matemático passo a passo.
*   **Interface Premium**: Design responsivo com efeitos de *glassmorphism* e *soft UI* otimizado para o tema escuro (Dark Mode).

---

## 🧮 Modelagem Matemática do Sistema

A calculadora toma decisões com base no custo de oportunidade e no custo marginal:

### 1. Custo Total Equivalente
Seja $M_k$ o volume de milhas na opção $k$, $D_k$ a coparticipação/taxa em dinheiro da opção $k$, e $V_m$ o valor do seu milheiro de referência. O custo total equivalente ($C_k$) é calculado por:

$$C_k = \left( \frac{M_k}{1000} \times V_m \right) + D_k$$

### 2. Custo Marginal do Milheiro Cobrado (Misto)
Tendo a opção de 100% pontos ($B$) como base de referência (maior volume de pontos e menor taxa de embarque), o valor cobrado pela cia aérea por milheiro nas opções mistas ($V_{cobrado, k}$) é:

$$V_{cobrado, k} = \frac{D_k - D_B}{\frac{M_B - M_k}{1000}}$$

*   Se $V_{cobrado, k} < V_m$: Vale a pena pagar em dinheiro e economizar as milhas.
*   Se $V_{cobrado, k} > V_m$: É preferível emitir com 100% Milhas.

---

## 🛠️ Tecnologias Utilizadas

1.  **Core**: HTML5 estrutural e JavaScript Vanilla (ES6+) para lógica matemática e controle de DOM.
2.  **Design e Estilização**: CSS3 customizado (Variáveis CSS, Flexbox, Grid, Glassmorphism, Micro-animações).
3.  **Processamento de Imagem**: **Tesseract.js** (Port do motor de redes neurais LSTM Tesseract do Google para Web Assembly).

---

## 🚀 Como Executar Localmente

Por ser uma aplicação totalmente *client-side*, não há necessidade de instalar dependências locais de backend ou configurar servidores.

1. Baixe os arquivos do projeto (`index.html` e `viaje-facil-brasil.png`).
2. Dê um duplo clique no arquivo `index.html` para abri-lo em qualquer navegador web moderno.
3. Insira o valor de referência do seu milheiro e utilize as funções de OCR ou entrada manual.

---

## 🌐 Hospedagem e Deploy (GitHub Pages)

Como a aplicação é composta apenas por arquivos estáticos (HTML, CSS e JS), ela pode ser hospedada gratuitamente e de forma extremamente estável no **GitHub Pages**.

### Passo 1: Ativar o GitHub Pages no Repositório
1. No seu repositório no GitHub, acesse a aba **Settings** (Configurações).
2. No menu lateral esquerdo, clique em **Pages**.
3. Em **Build and deployment** > **Source**, selecione a opção **Deploy from a branch**.
4. Em **Branch**, selecione a branch `main` e a pasta `/ (root)`.
5. Clique em **Save**.
6. Após alguns minutos, a calculadora estará publicada na web no endereço:
   `https://fsfariaspe.github.io/calculadora-milhas/`

### Passo 2: Apontar para um Subdomínio Personalizado (Opcional)
Para disponibilizar a ferramenta sob um subdomínio do seu site de portfólio (ex: `calculadora.seudominio.com`):
1. Acesse o painel de gerenciamento de DNS do seu domínio (Cloudflare, Registro.br, GoDaddy, etc.).
2. Adicione um novo registro de DNS com as seguintes configurações:
   * **Tipo**: `CNAME`
   * **Nome (Host)**: `calculadora` (ou o subdomínio escolhido)
   * **Destino (Target)**: `fsfariaspe.github.io`
   * **TTL**: Automático ou 3600
3. Volte para a aba **Pages** do seu repositório no GitHub.
4. No campo **Custom domain**, digite o subdomínio completo (ex: `calculadora.seudominio.com`) e clique em **Save**.
5. O GitHub irá provisionar um certificado SSL gratuito automaticamente para o seu subdomínio e criará um arquivo chamado `CNAME` no seu repositório para manter o redirecionamento ativo.
