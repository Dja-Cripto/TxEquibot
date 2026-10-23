# Integração Hibachi

## Fontes e SDK

O [portal oficial de desenvolvimento](https://docs.hibachi.xyz/hibachi-docs/api-and-developer-tools) aponta para a [referência API](https://api-doc.hibachi.xyz/), PyPI e o repositório `hibachi-xyz/yule-os`. Também foi localizado o [README do SDK Python](https://github.com/hibachi-xyz/hibachi_sdk/blob/main/python/README.md). Verificar qual repositório e versão são mantidos antes de fixar dependências; o código antigo não garante compatibilidade atual.

## Autenticação

As chamadas privadas exigem API key e Account ID. Operações assinadas precisam também do segredo de assinatura apropriado. A API key identifica/autentica; ela não substitui a assinatura. Segundo a documentação, a Private/Secret Key Hibachi não é a chave privada da carteira cripto. Não confundir os dois segredos.

Fontes: [Account API](https://hibachi-docs.redocly.app/accountapi), [coleção oficial e definições](https://www.postman.com/hibachi-xyz/hibachi-public/collection/kjruxq4/hibachi-api).

Credenciais devem ser criadas pelo usuário e armazenadas separadamente por conta. Confirmar opções reais de restrição, revogação e permissão de transferência. O executor do TxEquibot não deve implementar saques ou transferências na primeira versão.

## Hosts e chamadas necessárias

Host privado: `https://api.hibachi.xyz`. Mercado: `https://data-api.hibachi.xyz`. O SDK oferece consultas de instrumentos, preços, livro, conta, ordens, trades e settlements, além de criar/cancelar ordens.

| Função | Caminho REST |
|---|---|
| Instrumentos | `/market/exchange-info` |
| Preço e funding | `/market/data/prices` |
| Livro | `/market/data/orderbook` |
| Conta | `/trade/account/info` |
| Trades/settlements | `/trade/account/trades`, `/trade/account/settlements_history` |
| Ordem individual | `/trade/order` |
| Ordens da conta | `/trade/orders` |

Usar métodos e schemas específicos da [referência privada](https://hibachi-docs.redocly.app/accountapi) e do [SDK](https://github.com/hibachi-xyz/hibachi_sdk/blob/main/python/README.md). Confirmação de posição zerada é necessária após fechamento. Não presumir suporte a `reduceOnly` sem validar schema vigente e modo da conta.

## WebSockets

- Mercado: `wss://data-api.hibachi.xyz/ws/market`, sem autenticação. Oferece livro, preços, trades e estimativa de funding; implementar snapshot e atualizações corretamente. [Fonte](https://hibachi-docs.redocly.app/wsapi/market)
- Conta: `wss://api.hibachi.xyz/ws/account?accountId=...`, com `Authorization` contendo API key. Iniciar via `stream.start` e manter `stream.ping`; a documentação informa expiração após 10 segundos sem renovação. [Fonte](https://hibachi-docs.redocly.app/wsapi/account)
- Trading: `wss://api.hibachi.xyz/ws/trade?accountId=...`, autenticado. Métodos incluem criação, cancelamento, alteração e consulta de ordens. [Fonte](https://hibachi-docs.redocly.app/wsapi/trade)

A documentação de cancel-on-disconnect descreve cancelamento de ordens da conta, não encerramento de posições. Só habilitar após testar escopo e impacto em outras estratégias. [Fonte](https://www.postman.com/hibachi-xyz/hibachi-public/collection/6707f03b7c82ad6d2f10477c)

## Código anterior e pendências

Projeto local inspecionado: `separate local Hibachi prototype (not included in this repository)`. Contém `HibachiApiClient` e painel, mas não foi executado. Não copiar `.env`, configurações privadas ou pressupostos de funcionamento.

Confirmar: ambiente de teste disponível, limites REST/WS por IP e conta, precisão e mínimos, política de assinatura/nonce, semântica de fechamento e escopo das credenciais. Não inventar valores ausentes; a integração real depende dessas verificações.

