# LP10 · Chatbot para WhatsApp · ON Solutions Brasil

Landing page estática (HTML5 + CSS3 + JavaScript puro) para divulgação do serviço de
**chatbot para WhatsApp** da ON Solutions Brasil, com conversão via WhatsApp.

## Como usar

Abra `index.html` em um navegador. Não há build nem servidor necessário — é uma página
estática e independente.

## Estrutura

```text
index.html                         # Estrutura e conteúdo
css/styles.css                     # Estilos
js/main.js                         # Comportamento (Vanilla JS)
assets/img/                        # Favicon e logo (SVG)
DOCUMENTACAO-LP10-CHATBOT-WHATSAPP.md
```

## Configuração

- **WhatsApp:** número definido em `js/main.js` (`WA_NUMBER = "5511972243329"`).
- **Rastreamento:** preencha `ON_TRACKING` em `js/main.js` com os IDs de GTM, GA4 e Google
  Ads para ativar a medição. Por padrão, nada é carregado (sem IDs fictícios).

## Documentação

Detalhes completos de seções, funcionalidades, SEO, responsividade, acessibilidade, testes
e pendências em [`DOCUMENTACAO-LP10-CHATBOT-WHATSAPP.md`](./DOCUMENTACAO-LP10-CHATBOT-WHATSAPP.md).
