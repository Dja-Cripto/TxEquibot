# Integração TX Flow

## Acesso e transporte

Consultas usam `POST /info`; operações assinadas usam `POST /exchange`. Os streams `/ws` e `/api-ws` têm conjuntos distintos de canais. O onboarding documentado envolve depósito, aprovação de builder e autorização de agente. A rede principal exige conta na whitelist; a testnet não exige candidatura.

Fontes: [visão geral](https://docs.txflow.com/api/), [acesso Exchange](https://docs.txflow.com/api/exchange).

Hosts confirmados na [visão geral da API](https://docs.txflow.com/api/) (revisão de 23/10/2026): mainnet `https://rpc.txflow.com` e testnet `https://rpc.txflow-testnet.xyz`. O mesmo host serve `/info`, `/exchange`, `/ws`, `/api-ws`, `/ws-rtds` e, na testnet, o faucet (`POST /request-fund`). A ponte TxRelay tem host próprio (`https://api-bridge.txflow.com` / `https://devnet-bridge.txflow.net`). Nome de rede EIP-712: `TxFlow-Mainnet` / `TxFlow-Testnet`. Enviar `x-api-version: 2026-08-16` em `/info` e `/exchange`; confirmar a versão vigente no desenvolvimento. Host confirmado não significa acesso: a escrita na mainnet segue em fase de acesso limitado, sujeita a aprovação.

Leituras públicas (`perpMeta`, `activeAssetCtx`, `l2Book`) foram testadas a partir de um navegador na testnet em 23/10/2026 e responderam sem credenciais. Ordem de preparação da conta: depósito, `approveBuilderFee` para o builder usado, `approveAgent` para a chave que assina as ordens.

## Mapa mínimo

| Objetivo | Operação/tipo |
|---|---|
| Instrumentos e IDs | `perpMeta` |
| Livro e contexto | `l2Book`, `activeAssetCtx` |
| Posições e margem | `clearinghouseState` |
| Ordens pendentes | `frontendOpenOrders` |
| Execuções e funding | `userFills`, `userFundings` |
| Agentes | `approveAgent`, `approvedAgents`, `agentOwner` |
| Negociação | `order`, `cancel`, `cancelByCloid`, `modify2` |

Consultar os schemas específicos na [referência](https://docs.txflow.com/api/). Não assumir que respostas de snapshot e stream têm a mesma estrutura.

## Assinatura e segredos

A carteira titular autoriza; uma chave de agente assina trading. O domínio EIP-712 distingue mainnet (`869`) e testnet (`2511`). A assinatura de agente também envolve MessagePack, ordem de campos e nonce. Preços e quantidades são strings. Usar biblioteca validada ou reproduzir os vetores oficiais antes de enviar ordens. Centralizar geração de nonces por signer para impedir colisões no mesmo milissegundo.

Fontes: [Signing e vetores](https://docs.txflow.com/api/signing), [aprovar e revogar agente](https://docs.txflow.com/api/exchange/approveAgent).

Guardar no executor: referência segura à chave do agente. Configuração: endereço titular, endereço do agente, rede e versão. Nunca solicitar seed phrase. Verificar permissões efetivas do agente; não presumir que toda ação assinada por agente é apenas criação de ordem.

## Ordens

`order` recebe instrumento `a`, direção `b`, preço `p`, quantidade `s`, tipo `t`, identificador opcional `c`, margem `m` e redução `r`. Explicitar modo de margem. Para encerrar, usar redução quando aplicável e consultar a posição remanescente. Não inverter a posição por erro de tamanho. O schema tem até 50 ordens por ação; sucesso de envio não substitui confirmação de fills.

Fonte: [schema de ordem](https://docs.txflow.com/api/exchange/order).

## Builder Code

Fonte: [Builder Code](https://docs.txflow.com/getting-started/builder-code). Objeto de nível de ação `builder { b, f }` ao lado de `orders`, coberto pela assinatura. `f` está em décimos de ponto-base (rate = f / 100.000): `f=10` é 1 bp, `f=100` é 10 bp (0,1%). Tetos: perpétuos `f <= 100`, mercados de resultado `f <= 1000`. A taxa é adicional à taxa da corretora. O usuário aprova um teto com `approveBuilderFee` assinado pela chave principal (um agente não pode); até 20 builders por usuário; revogável com `revokeBuilderFee`. Taxa ausente, não aprovada ou acima do teto é ignorada sem rejeitar a ordem, então nunca presumir que foi cobrada. O endereço do builder precisa de pelo menos 100 USDC na conta de perps para acumular; `builderState` mostra acúmulo e elegibilidade; `claimBuilderRewards` é assinado por agente. A documentação lista `maxBuilderFee` para checar a aprovação, mas também diz que não há consulta por aprovação individual: guardar o teto solicitado a cada usuário e confirmar o comportamento.

## Funding

Fonte: [Funding](https://docs.txflow.com/trade/funding). Liquidação em ciclo fixo (padrão: a cada hora), pago entre traders, não à corretora. A taxa vem do oráculo e é lida em `activeAssetCtx` (campos de funding), expressa em percentual. Esse é o insumo do gate de edge mínimo.

## Limites e continuidade

Por IP: `/info` 50 requisições/s; `/exchange` 10/s; 10 conexões em cada endpoint WS. Respeitar `429` e `Retry-After`, compartilhar conexões e aplicar backoff. Em timeout ambíguo, reconciliar antes de repetir. Num servidor com vários usuários, os limites por IP são compartilhados.

Fonte: [limites](https://docs.txflow.com/api/rate-limits).

## Pendente

Confirmar biblioteca mantida e compatível (a documentação é publicada em Markdown para agentes de código em [llms.txt](https://docs.txflow.com/llms.txt)), acesso do projeto à escrita na mainnet, canal de fills e seus schemas, regras do ativo, taxas e faixas de taxa atuais (`userFees`, `feeTierRates`), a API do spot (o padrão TIP 1 está marcado como instável) e o comportamento de `maxBuilderFee`. A antiga URL `/api/sdk` retornou 404 nesta pesquisa; não tratar um nome de pacote mencionado anteriormente como dependência já validada.

[Candidatura](https://txflow.com/apply) · [Termos](https://txflow.com/terms)
