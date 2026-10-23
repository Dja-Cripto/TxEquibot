# Checklist para implementar

## Definições ainda necessárias

- Ativo inicial e contratos compatíveis em cada plataforma.
- Capital por plataforma e limite de perda; alavancagem e margem.
- Duração escolhida por ciclo: 5h, 12h ou outra; intervalo e limite de ciclos.
- Direção inicial manual; critérios para escolher automaticamente no futuro.
- Slippage, idade máxima dos dados, delta tolerado e tempo máximo sem hedge.
- Política para falha de entrada e de encerramento.
- Taxas e custos aceitáveis de entrada + saída; objetivo econômico da estratégia.

## TX Flow

- Obter acesso mainnet e confirmação escrita do uso automatizado.
- Confirmar host, API version, biblioteca e schemas atuais.
- Validar depósito/onboarding, builder aplicável e agente dedicado.
- Validar assinatura contra vetores, nonces únicos e revogação.

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
