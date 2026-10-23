# APIs, streams e webhooks

## Separação proposta

Painel web → serviço autenticado → executor persistente → adaptadores TX Flow e Hibachi. Banco guarda estratégias, ciclos, ordens, fills, funding, checkpoints e incidentes. Cofre separado guarda segredos delegados por usuário. Streams alimentam o executor; o painel recebe atualizações do serviço.

As referências consultadas descrevem REST e WebSocket. Não foi confirmado webhook nativo de notificação de fills nessas fontes. Por isso, um webhook não é pré-requisito para operar: a confirmação virá das APIs e streams, com reconciliação.

## Contrato interno proposto dos adaptadores

Operações: descobrir instrumentos, consultar livro/preços/funding, consultar conta/posições/ordens/fills, enviar ordem, cancelar ordem e assinar streams. Retornar capacidades explícitas como suporte a redução, identificador do cliente e sandbox. Estas são interfaces do nosso produto, não nomes de endpoints das exchanges.

Normalizar instrumento, multiplicador, unidade base, moeda de cotação, quantidade decimal, status, horário de origem e horário de recebimento. Preservar resposta original sanitizada para diagnóstico. Stablecoins distintas não devem ser tratadas como equivalentes perfeitas: mostrar risco de moeda e identificar conversão usada no resultado agregado.

Persistir intenção antes de envio; confirmar fills antes de atualizar exposição. Banco é a trilha durável, mas a posição observada na exchange é reconciliada antes de decisões após uma interrupção. Exclusividade por estratégia e isolamento entre usuários são obrigatórios.

## Alertas por webhook — opcionais, a implementar

Eventos sugeridos: `cycle.started`, `cycle.hedged`, `cycle.closing`, `cycle.completed`, `risk.unhedged`, `risk.margin_low`, `connection.lost`, `strategy.paused`.

Payload interno: versão, identificador único do evento, usuário/estratégia/ciclo, timestamp UTC, tipo e dados sanitizados. Não incluir segredos ou assinatura de ordens. Entrega após persistência via outbox, com tentativas limitadas, timeout e deduplicação. Alertas não podem bloquear o executor.

Para integrações externas, assinar payload com HMAC e timestamp, validar replay e idempotência e proteger destinos contra acesso a redes internas. Chaves de webhook são separadas das chaves de negociação. Nenhuma mensagem será enviada até o usuário configurar e autorizar um destino.

Sinais de entrada por webhook, como TradingView, ficam fora do MVP. Se forem adicionados, entram como intenções autenticadas sujeitas aos mesmos limites, nunca como bypass dos controles de risco.

