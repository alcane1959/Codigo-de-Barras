# Code Studio

Aplicação web para gerar, visualizar, salvar e exportar códigos de barras e QR Codes diretamente no navegador.

## Sobre o projeto

O **Code Studio** reúne diferentes padrões de códigos lineares e QR Code em uma interface responsiva. O usuário pode informar o conteúdo, adicionar descrição e preço, ajustar dimensões e cores, visualizar o resultado e baixar o código gerado.

A aplicação também oferece histórico local, backup e importação em JSON, impressão e alternância entre temas claro e escuro.

## Funcionalidades

- Geração de códigos de barras e QR Codes.
- Pré-visualização em tempo real.
- Validação conforme o padrão selecionado.
- Personalização da largura e altura das barras.
- Ajuste do tamanho do QR Code.
- Escolha da cor do código e da cor de fundo.
- Opção para mostrar ou ocultar o conteúdo abaixo das barras.
- Inclusão de descrição e preço na etiqueta.
- Download em PNG.
- Download em SVG para códigos lineares.
- Impressão da etiqueta.
- Histórico armazenado no navegador.
- Reutilização e exclusão de itens do histórico.
- Exportação do histórico para backup JSON.
- Importação de backup com validação e remoção de duplicados.
- Alternância entre tema claro e escuro.
- Interface responsiva para computadores e dispositivos móveis.

## Tipos de código compatíveis

| Tipo | Regras principais |
|---|---|
| CODE 128 | Caracteres ASCII imprimíveis |
| EAN-13 | 12 ou 13 números |
| UPC-A | 11 ou 12 números |
| CODE 39 | Letras A-Z, números, espaço e símbolos permitidos pelo padrão |
| ITF-14 | 13 ou 14 números |
| MSI | Somente números |
| QR Code | Conteúdo UTF-8, incluindo acentos, símbolos, emojis, textos, links e contatos |

## Tecnologias utilizadas

- HTML5
- CSS3
- JavaScript Vanilla
- Web Storage API (`localStorage`)
- Canvas API
- SVG
- Blob e FileReader APIs
- JsBarcode
- qrcode-generator

## Estrutura do projeto

```text
code-studio/
├── index.html
└── README.md
```

A interface, os estilos e a lógica da aplicação estão concentrados no arquivo `index.html`.

## Como executar

1. Baixe os arquivos do projeto.
2. Abra o arquivo `index.html` em um navegador moderno com acesso à internet.
3. Selecione o tipo de código.
4. Informe o conteúdo a ser codificado.
5. Preencha opcionalmente a descrição e o preço.
6. Ajuste as dimensões e as cores.
7. Clique em **Gerar código**.
8. Use as ações disponíveis para baixar, imprimir ou salvar no histórico.

Não é necessário instalar pacotes ou executar um processo de compilação.

## Dependências externas

O projeto carrega as seguintes bibliotecas por CDN:

- **JsBarcode 3.12.3**, usada na geração dos códigos de barras lineares.
- **qrcode-generator 1.4.4**, usada na geração de QR Codes.

Sem conexão com a internet, essas bibliotecas podem não ser carregadas e a geração dos códigos pode não funcionar.

## Validação dos dados

Cada formato aplica regras próprias antes da geração. A interface mostra mensagens quando o conteúdo está vazio, excede o tamanho apropriado ou contém caracteres incompatíveis.

Para códigos lineares, conteúdos com mais de 80 caracteres são direcionados ao uso de QR Code, pois códigos muito extensos podem ficar largos e difíceis de ler.

## Exportação

### PNG

Códigos lineares são renderizados em SVG e convertidos para PNG com escala ampliada. QR Codes são gerados em `canvas` e baixados diretamente em PNG.

### SVG

A exportação em SVG está disponível para os códigos lineares. Essa opção fica oculta quando o tipo selecionado é QR Code.

### Impressão

A impressão utiliza uma folha de estilos específica, ocultando controles, histórico, cabeçalho e rodapé para destacar apenas a etiqueta gerada.

## Histórico local

Os códigos salvos ficam armazenados no `localStorage` com a chave:

```text
codeStudioHistory
```

O histórico principal mantém até 15 itens. Cada registro contém:

- tipo do código;
- conteúdo;
- descrição;
- preço;
- identificador local.

Os dados permanecem vinculados ao navegador e ao dispositivo utilizados. A limpeza dos dados do navegador pode remover o histórico.

## Backup e restauração

### Fazer backup

O botão **Fazer backup** exporta o histórico para um arquivo JSON contendo a identificação do aplicativo, a versão do formato, a data de exportação e os códigos salvos.

### Importar backup

O botão **Importar backup** aceita um arquivo JSON, valida os registros, limita os campos e ignora duplicidades com o mesmo tipo e conteúdo. A lista resultante é limitada a 500 registros durante a importação.

> Antes de importar, mantenha uma cópia do histórico atual. A aplicação mescla os registros válidos do arquivo com os itens existentes.

## Tema visual

O botão de tema alterna entre os modos claro e escuro durante a sessão. As cores são controladas por variáveis CSS no seletor `:root` e no atributo `data-theme="dark"`.

## Compatibilidade

Use um navegador moderno com suporte a:

- JavaScript;
- `localStorage`;
- Canvas API;
- SVG;
- Blob e Object URLs;
- FileReader;
- atributo `download`;
- campos de cor e intervalo do HTML5.

## Limitações

- As bibliotecas de geração são carregadas pela internet.
- O histórico não é sincronizado entre dispositivos.
- Não há autenticação ou banco de dados remoto.
- O tema escolhido não é persistido após o fechamento da página.
- A leitura correta dos códigos depende da qualidade da exportação, do conteúdo e da compatibilidade do leitor utilizado.

## Autor

**Alberto de Campos Neto**

## Aviso

> Este projeto é uma demonstração educacional desenvolvida para estudos de HTML, CSS e JavaScript. A empresa mencionada é fictícia e qualquer semelhança com empresas reais é mera coincidência.
