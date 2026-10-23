# Checklist para implementar

## Definições ainda necessárias

- Ativo inicial e contratos compatíveis em cada plataforma.
- Capital por plataforma e limite de perda; alavancagem e margem.
- Duração escolhida por ciclo: 5h, 12h ou outra; intervalo e limite de ciclos.
- Direção inicial manual; critérios para escolher automaticamente no futuro.
- Slippage, idade máxima dos dados, delta tolerado e tempo máximo sem hedge.
- Política para falha de entrada e de encerramento.
- Taxas e custos aceitáveis de entrada + saída; objetivo econômico da estratégia.
- Múltiplo exigido do gate de edge mínimo (carry esperado ÷ custos) e fonte do funding usado na decisão.

## TX Flow

- Obter acesso de escrita na mainnet e confirmação escrita do uso automatizado, incluindo estratégias hedgeadas.
- Host da mainnet (`https://rpc.txflow.com`) e da testnet (`https://rpc.txflow-testnet.xyz`) confirmados na documentação em 23/10/2026; reconfirmar API version, biblioteca e schemas atuais.
- Validar na testnet, sem candidatura: depósito (faucet), `approveBuilderFee`, agente dedicado e ordens.
- Validar assinatura contra vetores, nonces únicos e revogação.
- Decidir a taxa de builder (pode ser zero no piloto), o teto dentro do limite de 0,1% em perpétuos e a exibição da soma ao usuário.
- Preparar o endereço de builder: mínimo de 100 USDC na conta de perps para acumular; testar `builderState`.
- Confirmar o comportamento de aprovação ausente ou revogada (a taxa é ignorada sem rejeição).
- Confirmar se há API estável de spot para uma proteção spot–perpétuo dentro do TX Flow.

## Hibachi

- Confirmar referência/SDK mantido e versão compatível.
- Criar credenciais corretas e confirmar permissões e revogação.
- Confirmar limites por IP/conta, ambiente de teste e assinatura.
- Validar contrato, precisão, funding e fechamento sem inversão acidental.

## Produto e operação

- Implementar primeiro consulta e painel, depois execução em testes.
- Fixar dependências verificadas; não reutilizar cegamente o scalper antigo.
- Não reutilizar escolhas aleatórias de direção do scalper para suposto hedge.
- Isolar usuários e credenciais; omitir segredos de logs e repositório.
- Persistir ciclos/horários e reconciliar após reinício ou timeout.
- Demonstrar encerramento das duas pernas e bloqueio de ciclo sobreposto.
- Validar contabilização sem taxas ou slippage descontados duas vezes.
- Revisar interface para falhas, dados antigos e proteção incompleta.
- Confirmar continuidade do executor e recuperação do banco.

Este checklist registra pendências reais. O kit não substitui aprovação de acesso, credenciais do usuário ou validação funcional.
