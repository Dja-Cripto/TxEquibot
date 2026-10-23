# Estratégia de ciclos temporizados

## Requisito do usuário

Operar nos dois sentidos entre Hibachi e TX Flow: comprado em uma e vendido na outra. Manter por duração configurável, como 5 ou 12 horas, encerrar as duas pernas e repetir. A direção inicial poderá ser TX Flow comprado/Hibachi vendido ou o inverso. Escolher direção manualmente no piloto; seleção automática por funding/spread exige regra econômica própria.

Proposta: duração fixa por ciclo no MVP. Cinco e doze horas são exemplos de escolha, não extremos de uma distribuição aleatória. Não randomizar duração ou inverter direção automaticamente sem configuração explícita.

## Fluxo e relógio

`AGUARDANDO → VALIDANDO → ABRINDO → PROTEGIDO → ENCERRANDO → RECONCILIANDO → CONCLUÍDO → AGUARDANDO`

Falhas podem levar a `RECUPERANDO` ou `INTERVENÇÃO`; nunca saltar para um novo ciclo com exposição desconhecida.

1. Reservar o ciclo persistente e adquirir exclusividade da estratégia.
2. Verificar autorizações, margem, ativos compatíveis, dados recentes, limites e custos.
3. Coordenar ordens de entrada. Confirmar fills e delta dentro da tolerância.
4. Persistir `protected_at` em UTC e `scheduled_close_at = protected_at + hold_duration_seconds`. O prazo não começa no clique nem no envio da primeira ordem.
5. Monitorar continuamente as duas contas; cinco ou doze horas não significam ficar sem verificar margem.
6. Ao vencer o prazo, iniciar fechamento coordenado; antecipar por regra de risco. O horário é de início da tentativa de encerramento, sem garantia de execução exata.
7. Cancelar somente ordens do ciclo, consultar posições atuais, reduzir quantidades pertencentes à estratégia e confirmar ambas zeradas dentro da precisão do instrumento. Tratar resíduos abaixo do mínimo explicitamente.
8. Consolidar fills, funding e taxas. Marcar concluído apenas após reconciliação.
9. Revalidar condições, respeitar intervalo e limites e iniciar o próximo ciclo se repetição ainda estiver habilitada.

Se não existir tamanho comum executável dentro da tolerância de delta, não abrir. Confirmar previamente arredondamento compatível entre plataformas.

## Condições para repetição

Repetição é uma preferência, não uma obrigação de abrir a qualquer custo. Bloquear nova entrada se houver posição residual, ordens pendentes, margem insuficiente, custos acima do limite, preço antigo, incidente, perda limite atingida ou autorização revogada. Permitir limite de ciclos e parada após o ciclo atual.

No MVP, usar conta/subconta dedicada quando disponível e proibir operações manuais concorrentes nos mesmos instrumentos. Se a plataforma agrega posições, atribuição por estratégia precisa ser comprovada antes de permitir compartilhamento.

## Recuperação

- Uma perna falhou: proteger o preenchimento real ou desfazer a perna executada segundo política limitada por prazo, slippage e exposição.
- Fechamento parcial: continuar monitorando e reduzindo o saldo; não considerar concluído.
- Reinício antes do prazo: carregar ciclo persistido, reconciliar e continuar o relógio original.
- Reinício após o prazo: reconciliar e priorizar fechamento; não esperar outras 5/12 horas.
- API indisponível: bloquear novas entradas, manter o incidente visível e tentar recuperação limitada. Sem API disponível não existe garantia de encerramento.
- Pausa: interrompe novas entradas; posições abertas continuam sob monitoramento e política de saída.

## Painel

Mostrar as duas pernas, delta, margem por plataforma, tempo protegido, contagem regressiva, horário previsto, resultado e status de repetição. Ações: pausar novas entradas, parar após este ciclo e encerrar agora. Encerrar agora não é sinônimo de cancelar ordens.

## Validação obrigatória

Simular relógio para 5 e 12 horas; confirmar ausência de reinício de prazo após falha. Validar fills parciais, rejeição, timeout ambíguo, revogação, desconexão, encerramento incompleto e disputa entre dois executores. Depois validar em ambientes de teste equivalentes. Não usar dinheiro real para compensar ausência de sandbox de uma das plataformas.

