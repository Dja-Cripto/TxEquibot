# Integração TX Flow

## Acesso e transporte

Consultas usam `POST /info`; operações assinadas usam `POST /exchange`. Os streams `/ws` e `/api-ws` têm conjuntos distintos de canais. O onboarding documentado envolve depósito, aprovação de builder e autorização de agente. A rede principal exige conta na whitelist; a testnet não exige candidatura.

Fontes: [visão geral](https://docs.txflow.com/api/), [acesso Exchange](https://docs.txflow.com/api/exchange).

Endpoint de teste confirmado nos exemplos de ordem: `https://rpc.txflow-testnet.xyz/exchange`; consultas no mesmo host, caminho `/info`. O exemplo oficial usa `x-api-version: 2026-08-16`. Confirmar versão vigente no desenvolvimento. Host da mainnet: pendente de confirmação oficial no onboarding; não deduzir pelo nome da testnet.

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

## Limites e continuidade

Por IP: `/info` 50 requisições/s; `/exchange` 10/s; 10 conexões em cada endpoint WS. Respeitar `429` e `Retry-After`, compartilhar conexões e aplicar backoff. Em timeout ambíguo, reconciliar antes de repetir. Num servidor com vários usuários, os limites por IP são compartilhados.

Fonte: [limites](https://docs.txflow.com/api/rate-limits).

## Pendente

Confirmar host mainnet, biblioteca mantida e compatível, acesso do projeto, canal de fills e seus schemas, regras do ativo, taxas atuais e fluxo de builder aplicável. A antiga URL `/api/sdk` retornou 404 nesta pesquisa; não tratar um nome de pacote mencionado anteriormente como dependência já validada.

[Candidatura](https://txflow.com/apply) · [Termos](https://txflow.com/terms)
