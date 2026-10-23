# TxEquibot — kit de integração

> Pesquisa técnica de apoio ao foco atual: ciclos delta neutros com o TX Flow como plataforma principal e uma segunda perna por adaptador (Hibachi é a candidata estudada). Consulte o README principal para o escopo vigente, o gate de edge mínimo e o Builder Code.

Pesquisa realizada em 23/10/2026. Material de preparação, não um robô executável. Nenhuma credencial foi copiada do projeto anterior e nenhuma ordem foi enviada.

## Arquivos

- [TXFLOW.md](TXFLOW.md): acesso, assinatura, consultas e operações.
- [HIBACHI.md](HIBACHI.md): autenticação, SDK, REST e streams.
- [CICLOS.md](CICLOS.md): funcionamento por períodos, repetição e recuperação.
- [ARQUITETURA-E-EVENTOS.md](ARQUITETURA-E-EVENTOS.md): adaptadores, persistência, WebSocket e webhooks opcionais.
- [CHECKLIST.md](CHECKLIST.md): decisões e validações antes da implementação real.
- [config.exemplo.json](config.exemplo.json): configuração ilustrativa, com operações reais desativadas e limites ainda não definidos.

Recomendação para o primeiro piloto: um ativo, um ciclo por usuário, posições dedicadas ao robô e um executor persistente. Interface web apenas controla e acompanha esse executor.

Não há uma integração autenticada pronta neste kit. Os hosts do TX Flow estão confirmados na documentação oficial (revisão de 23/10/2026), mas ambientes, versões, assinatura e permissões de cada plataforma devem ser validados antes de operar. Não confundir testnet TX Flow com produção Hibachi: nunca combinar uma perna simulada com outra real para tentar produzir hedge.

O período de permanência é uma regra operacional; não assegura rentabilidade. Cada abertura e fechamento tem custos (taxas em quatro execuções, eventual taxa de builder e slippage), e o único retorno esperado é o diferencial de funding. Por isso o ciclo só abre se o carry esperado cobrir os custos (gate de edge mínimo). Os limites de perda ainda precisam ser definidos.
