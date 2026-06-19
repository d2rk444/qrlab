# QR Lab

QR Lab é uma página web simples, leve e responsiva para gerar QR Codes a partir de texto ou arquivos pequenos. O projeto funciona em um único arquivo `index.html`, sem necessidade de servidor, banco de dados ou instalação local.

A aplicação calcula automaticamente a capacidade do QR Code, escolhe a menor versão possível e bloqueia arquivos acima do limite seguro. Também possui interface bilíngue em Português e Inglês, além de alternância entre tema claro e escuro.

## Demonstração

Para usar localmente, basta abrir o arquivo:

```text
index.html
```

Também é possível publicar diretamente com GitHub Pages.

## Funcionalidades

- Geração de QR Code para texto, URL, token, configuração simples e outros conteúdos curtos.
- Geração de QR Code para arquivo pequeno, com conversão para Base64/Data URI.
- Bloqueio automático de arquivos maiores que a capacidade atual do QR Code.
- Seleção entre entrada de texto ou arquivo pequeno.
- Seleção do nível de correção de erro: L, M, Q e H.
- Seleção automática ou manual da versão do QR Code, de V1 até V40.
- Cálculo de bytes, versão, módulos e uso da capacidade.
- Pré-visualização do QR Code antes do download.
- Download do QR Code em PNG.
- Alternância entre Português e Inglês.
- Alternância entre tema claro e tema escuro.
- Layout minimalista, responsivo e sem dependência de backend.

## Como usar

1. Abra o arquivo `index.html` no navegador.
2. Escolha o tipo de entrada:
   - `Texto`
   - `Arquivo pequeno`
3. Informe o conteúdo ou selecione um arquivo dentro do limite exibido.
4. Ajuste, se necessário:
   - correção de erro;
   - versão do QR Code;
   - tamanho do PNG;
   - cores do QR Code e do fundo.
5. Clique em `Gerar QR`.
6. Clique em `Baixar PNG` para salvar a imagem.

## Limite de arquivos

O projeto foi pensado para arquivos pequenos. Ele não divide arquivos grandes em vários QR Codes.

O tamanho máximo aceito muda conforme:

- versão do QR Code;
- nível de correção de erro;
- tamanho final do conteúdo após conversão para Base64/Data URI.

Como Base64 aumenta o tamanho do conteúdo, o limite real do arquivo original é menor que a capacidade bruta do QR Code. Por isso a página exibe o limite máximo aproximado antes do upload e recusa automaticamente arquivos maiores.

Arquivos recomendados:

- TXT;
- CSV pequeno;
- JSON pequeno;
- XML pequeno;
- SVG pequeno;
- configurações leves;
- tokens ou chaves curtas.

Arquivos não recomendados:

- imagens grandes;
- PDFs;
- vídeos;
- planilhas grandes;
- arquivos compactados;
- documentos extensos.

Para arquivos grandes, o ideal é hospedar o arquivo em um serviço externo e gerar um QR Code apenas com o link.

## Modelo matemático usado

O QR Code possui versões de 1 a 40. Cada versão aumenta a quantidade de módulos por lado.

```text
módulos por lado = 4 × versão + 17
```

Exemplos:

| Versão | Módulos por lado |
|---:|---:|
| V1 | 21 × 21 |
| V10 | 57 × 57 |
| V20 | 97 × 97 |
| V30 | 137 × 137 |
| V40 | 177 × 177 |

A aplicação mede o conteúdo em bytes UTF-8 e procura a menor versão capaz de armazenar esse conteúdo no nível de correção selecionado.

## Correção de erro

O QR Code usa correção de erro para continuar legível mesmo com pequenas falhas, sujeira, perda visual ou baixa qualidade de impressão.

| Nível | Recuperação aproximada | Uso recomendado |
|---|---:|---|
| L | 7% | maior capacidade, menor proteção |
| M | 15% | uso geral recomendado |
| Q | 25% | melhor para impressão ou leitura difícil |
| H | 30% | maior proteção, menor capacidade |

Quanto maior a correção de erro, menor a quantidade de dados que cabe no QR Code.

## Capacidade máxima teórica

A capacidade máxima depende do modo de codificação. Para QR Code padrão em sua maior versão, V40, com correção de erro baixa, os limites teóricos aproximados são:

| Tipo de conteúdo | Capacidade máxima aproximada |
|---|---:|
| Numérico | 7.089 caracteres |
| Alfanumérico | 4.296 caracteres |
| Bytes | 2.953 bytes |
| Kanji | 1.817 caracteres |

Na prática, recomenda-se usar muito menos que o limite máximo para manter boa leitura em celulares, impressões e telas pequenas.

## Estrutura do projeto

```text
qr-lab/
├── index.html
└── README.md
```

## Tecnologias

- HTML5
- CSS3
- JavaScript puro
- Biblioteca `qrcode-generator`
- LocalStorage para idioma e tema
- FileReader API para leitura de arquivos pequenos
- TextEncoder para cálculo em bytes UTF-8

## Observações importantes

- O projeto roda totalmente no navegador.
- Nenhum arquivo é enviado para servidor.
- O arquivo selecionado é processado localmente.
- O QR Code gerado pode conter dados sensíveis caso você insira senhas, tokens ou chaves.
- Para segurança, evite compartilhar QR Codes com informações privadas.

## Melhorias futuras

- Exportação em SVG.
- Modo PWA para instalação no dispositivo.
- Histórico local opcional.
- Validação específica para Wi-Fi, vCard e e-mail.
- Campo dedicado para gerar QR Code de links encurtados.

## Licença / License

Copyright (c) 2026 d2rk444. Todos os direitos reservados / All rights reserved.

**PT-BR:** Este projeto é protegido por direitos autorais. É permitido o uso pessoal ou comercial da ferramenta. No entanto, é **estritamente proibida** a redistribuição, sublicenciamento, espelhamento do código ou venda do software e de seus derivados sem autorização prévia por escrito. Consulte o arquivo `LICENSE` para ler os termos completos.

**EN:** This project is protected by copyright. Personal or commercial use of the tool is allowed. However, redistribution, sublicensing, mirroring of the code, or sale of the software and its derivatives is **strictly prohibited** without prior written authorization. See the `LICENSE` file for full terms.
