# FlyMiles Calculator: Calculadora Inteligente de Emissões (Milhas vs. Dinheiro)

A **FlyMiles Calculator** é um utilitário web de produtividade pessoal de alta performance desenvolvido para otimizar e automatizar a comparação financeira de emissões de passagens aéreas. O sistema ajuda a responder de forma instantânea a pergunta clássica de todo milheiro: **vale a pena emitir com milhas puras, milhas + dinheiro (coparticipação) ou pagar a passagem 100% em dinheiro?**

O grande diferencial da ferramenta é a automação da entrada de dados por meio de **Reconhecimento Óptico de Caracteres (OCR) executado diretamente no navegador do cliente (client-side)**, eliminando a digitação manual de múltiplos valores de pontos e taxas de embarque.

---

## ✨ Principais Funcionalidades

*   **Importação por Print (OCR Local)**: Copie a tela de busca da sua companhia aérea e cole diretamente na ferramenta com `Ctrl+V` (ou clique para enviar a imagem). O processamento ocorre 100% no seu computador, de forma segura e instantânea.
*   **Algoritmo de Pareamento por Proximidade**: Resolve problemas comuns de OCR (como desalinhamento de colunas de texto) associando inteligentemente cada bloco de milhas com a coparticipação correspondente da mesma opção de forma espacial.
*   **Heurística Corretiva de Domínio (Smiles 30% Ratio)**: Identifica e corrige erros clássicos de leitura óptica da Smiles (como ler a tarifa mista de `9.570 milhas` como `2.570 milhas`) validando proporções matemáticas pré-definidas em relação à passagem base.
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

## 🚀 Como Executar

Por ser uma aplicação totalmente *client-side*, não há necessidade de instalar dependências locais de backend ou configurar servidores.

1. Baixe os arquivos do projeto (`index.html` e `logo-placeholder.png`).
2. Dê um duplo clique no arquivo `index.html` para abri-lo em qualquer navegador web moderno.
3. Insira o valor de referência do seu milheiro.
4. Capture o print da tela de emissão da companhia aérea (Azul, Smiles ou LATAM) e cole com `Ctrl+V` dentro da página para que ela preencha o formulário e faça as contas automaticamente.
