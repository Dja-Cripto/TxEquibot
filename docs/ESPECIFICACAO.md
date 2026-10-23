# TxEquibot — especificação de produto e implementação

> Documento de referência da expansão delta neutra. O MVP atual está definido nos documentos em inglês vinculados no README; esta especificação não representa o escopo da primeira entrega.

Data: 23 de outubro de 2026. Status: planejamento. Este documento registra a intenção do usuário e propõe decisões de implementação; não descreve funcionalidades já prontas. Parâmetros financeiros, segunda plataforma e infraestrutura continuam pendentes.

Atualização: o usuário definiu a Hibachi como segunda plataforma pretendida. Foi inspecionado um projeto Python anterior em `separate local Hibachi prototype (not included in this repository)`, com uso de `HibachiApiClient`, consultas de conta, envio de ordens e painel web local. Isso comprova existência de código de integração, não funcionamento atual, lançamento público ou execução delta neutra. Não foram executados scripts nem enviadas ordens nessa inspeção. As referências abaixo à escolha da segunda plataforma passam a significar validação técnica da integração Hibachi.

## 1. Objetivo e escopo confirmado

Criar um robô de trading com foco em posições delta neutras entre o TX Flow e uma segunda plataforma. O produto deve permitir uso pelo criador e, posteriormente, por outras pessoas, com uma interface bonita, clara e acessível.

O robô deve combinar execução de operações, gestão de portfólio e acompanhamento de resultados. A experiência precisa explicar o estado real das posições, inclusive quando a proteção estiver incompleta.

Delta neutro significa buscar compensação da exposição direcional. Não significa ausência de risco: margem, liquidação, funding, diferença de preços, liquidez e indisponibilidade existem separadamente em cada plataforma.

## 2. Formato recomendado: aplicação web com execução contínua

Recomendação inicial: painel online responsivo, com processamento do robô em um serviço separado do navegador. A pessoa acessa o site, conecta sua carteira, vincula a segunda plataforma, concede as autorizações necessárias e configura a estratégia. A execução pode continuar com o navegador fechado enquanto o serviço estiver disponível.

Conectar a carteira identifica um endereço; não concede automaticamente permissão para negociar. Consultar dados, autenticar uma sessão, aprovar um agente e iniciar uma estratégia são ações diferentes e devem aparecer separadamente na experiência.

O TX Flow documenta agentes autorizados pelo titular para assinar operações. A integração precisa confirmar o estado da conta e as etapas de autorização vigentes. A segunda plataforma pode exigir outra carteira ou credenciais próprias; uma conexão não habilita automaticamente as duas.

| Alternativa | Benefício | Limitação | Decisão proposta |
|---|---|---|---|
| Site com execução apenas no navegador | Distribuição simples | Fechar a aba, suspender o aparelho ou perder a conexão interrompe a execução | Somente demonstração ou monitoramento |
| Site com executor em servidor | Acesso fácil e operação independente da aba | Exige operação contínua e proteção rigorosa das credenciais delegadas | Produto inicial recomendado |
| Aplicativo instalado com executor local | Credenciais podem permanecer no computador | Depende de energia, conexão e atualizações no aparelho | Possível opção futura |
| Painel web com executor instalado pelo usuário | Painel central com execução sob controle do usuário | Instalação e suporte mais complexos | Possível evolução avançada |

Não construir site e aplicativo desktop simultaneamente no primeiro lançamento. Se a decisão for não manter nenhuma chave delegada no servidor, revisar a arquitetura e priorizar o executor local antes de implementar trading contínuo.

## 3. Jornada da pessoa usuária

1. Abrir a apresentação do produto e acessar uma demonstração com dados explicitamente simulados ou conectar a carteira.
2. Assinar uma mensagem de autenticação com desafio único, validade curta e domínio correto. A conexão isolada não autentica alterações de conta.
3. Visualizar os dados da conta vinculada no TX Flow, com horário da última atualização e ambiente claramente identificado.
4. Conectar a segunda plataforma e verificar as permissões realmente disponíveis.
5. Autorizar o agente de negociação e visualizar como revogar o acesso. Etapas de depósito e eventuais Builder Fees devem ser explicadas e aprovadas separadamente quando exigidas.
6. Escolher um instrumento compatível nas duas plataformas e configurar capital por plataforma, limites e condições de entrada e saída.
7. Revisar um resumo: lados das posições, quantidades, exposição, custos estimados e comportamento se uma perna falhar.
8. Iniciar explicitamente a estratégia. Conectar a carteira nunca inicia operações por conta própria.
9. Acompanhar posições, margem, resultado e eventos; pausar novas entradas ou solicitar encerramento coordenado.

## 4. Interface e direção visual propostas

Painel com aparência de produto financeiro profissional, tema escuro inicial, fundo grafite, superfícies discretas e uma cor de destaque para ações principais. Usar tipografia legível, espaçamento confortável e números alinhados. Ganhos e perdas precisam ter sinal e texto, sem depender apenas de verde e vermelho.

Priorizar o desktop para configuração e comparação de posições. No celular, manter acompanhamento, alertas e controles essenciais utilizáveis. Valores financeiros devem indicar unidade, moeda e se são estimativas.

Telas previstas:

- **Visão geral:** saldo por plataforma, exposição líquida, margem disponível, resultado e situação do robô.
- **Estratégias:** configuração, prévia e estado de cada estratégia; uma única estratégia por usuário no primeiro piloto.
- **Posições:** duas pernas lado a lado, quantidades, preços, funding, margem e execuções pendentes.
- **Resultados:** PnL realizado e não realizado, funding e taxas com períodos selecionáveis.
- **Atividade:** ordens, preenchimentos, rejeições, rebalanceamentos e intervenções, com horários.
- **Conexões e segurança:** plataformas, permissões, agente autorizado e instruções de revogação.

Estados visíveis: desconectado, somente leitura, aguardando autorização, pronto, entrando, protegido dentro da tolerância, proteção incompleta, pausado, encerrando e intervenção necessária. Uma conexão sem dados recentes não pode aparecer como saudável.

As ações **pausar novas entradas**, **cancelar ordens abertas** e **encerrar posições** devem ser distintas. Pausar não remove posições nem elimina sua necessidade de monitoramento. Encerrar deve apresentar uma confirmação contextual com as posições afetadas.

## 5. Estratégia e cálculo de exposição

Requisito atualizado: ciclos com duração configurável (exemplos: 5 ou 12 horas), encerramento coordenado e repetição somente após confirmar ambas as pernas encerradas. A contagem começa com as duas posições confirmadas e protegidas dentro da tolerância. Ver [kit de integração e regras de ciclo](../integracoes/README.md).

O mecanismo inicial coordena uma posição comprada e uma vendida no mesmo ativo econômico. Oportunidades de funding ou spread são possibilidades; a regra exata de seleção ainda precisa ser escolhida.

Para contratos lineares equivalentes, normalizar quantidades para unidades do ativo: delta líquido = quantidade comprada menos quantidade vendida. Estimar exposição em moeda usando um preço de referência identificado. Não comparar apenas a margem depositada ou o valor nominal informado por cada plataforma.

O adaptador deve validar multiplicador, tamanho mínimo, precisão, moeda de liquidação e regras do instrumento. Contratos inversos, opções e ativos apenas correlacionados ficam fora da primeira versão.

Antes de entrar, verificar saldo e margem em ambos os locais, dados recentes, profundidade, custo estimado das duas pernas e possibilidade de encerramento. Funding projetado deve aparecer como estimativa, normalizado para períodos comparáveis, sem promessa de continuidade.

Rebalancear apenas segundo tolerância e custo definidos. Não transferir fundos nem aumentar alavancagem automaticamente na primeira versão.

## 6. Execução e recuperação

As duas pernas não são atômicas. Implementar uma máquina de estados persistente por operação: planejada, validada, enviando, parcialmente executada, protegida, recuperando, encerrando, encerrada ou intervenção necessária.

Cada intenção recebe um identificador estável e cada ordem mantém vínculo com estratégia, usuário, plataforma e tentativa. Uma resposta de envio não equivale a preenchimento. Confirmar quantidades executadas e reconciliar ordens e posições após quedas ou reinícios.

Se uma perna executar parcialmente, proteger a quantidade efetivamente preenchida conforme os limites. Se a outra falhar, seguir a política configurada de tentativas limitadas ou redução da posição já aberta. Definir previamente prazo máximo sem proteção e slippage máximo; ao esgotá-los, bloquear novas entradas e sinalizar o incidente. Não existe garantia de fechamento imediato durante indisponibilidade de uma plataforma.

Em timeout com resultado desconhecido, consultar o estado antes de reenviar. Usar identificadores do cliente quando suportados, nonces únicos e prevenção de execução duplicada. Apenas um executor pode controlar uma estratégia por vez.

## 7. Gestão de risco e resultado

Parâmetros obrigatórios antes de qualquer piloto: capital por plataforma, posição máxima, alavancagem máxima, tolerância de delta, prazo sem proteção, idade máxima dos dados, slippage, margem mínima e limites de perda. Não adotar valores financeiros arbitrários como configuração aprovada.

Monitorar margem de cada conta independentemente do resultado agregado. Bloquear novas entradas em caso de dados desatualizados, autorização revogada, limite excedido ou falha de reconciliação.

Resultado do trading = PnL realizado + PnL não realizado + funding líquido − taxas efetivamente cobradas. Normalizar conforme os dados de cada API para não descontar taxas duas vezes. Depósitos e saques são fluxos de capital, não lucro. Slippage comparado ao preço de referência deve ser exibido como análise de execução; não descontá-lo novamente quando já refletido no PnL.

Pontos ou incentivos, se houver suporte futuro, ficam separados do lucro efetivamente realizado. Não fazer volume artificial nem depender de recompensas para apresentar rentabilidade.

## 8. Arquitetura técnica proposta

- **Interface web:** TypeScript e React; framework web a selecionar. Componentes acessíveis e gráficos com estados de carregamento, erro e ausência de dados.
- **Serviço da aplicação:** autenticação por carteira, usuários, configurações, permissões e entrega de atualizações ao painel.
- **Adaptadores de plataformas:** contrato comum para mercado, instrumentos, saldo, posições, ordens, preenchimentos e estado da conexão; implementações específicas para cada API.
- **Executor contínuo:** serviço persistente separado de páginas e funções de curta duração; máquina de estados, estratégia, risco e reconciliação.
- **Persistência:** banco relacional para configurações, intenções, ordens, fills, eventos e checkpoints; fila durável quando necessária. Precisão decimal para cálculos monetários, sem ponto flutuante binário como fonte de verdade.
- **Proteção de segredos:** chaves delegadas por usuário, criptografia com gestão de chaves separada e acesso restrito ao executor. Nunca registrar segredos em logs, repositório ou armazenamento do navegador.
- **Operação:** monitoramento de conexões, atraso dos dados, executor, reconciliação e falhas; backup e restauração verificados.

O usuário não entrega seed phrase nem chave principal da carteira. Credenciais da segunda plataforma devem ter o menor escopo possível e saques desativados quando suportado. Permissão para negociar ainda permite causar perdas; não apresentar isso como ausência de risco ou como fundos fora de qualquer controle delegado.

Limites locais do robô não devem ser apresentados como limites garantidos pelo protocolo. Confirmar quais restrições o agente realmente permite. Revogação precisa impedir novas ações e o painel deve explicar que posições existentes permanecem abertas.

Isolar dados e credenciais por usuário e verificar autorização no servidor em cada operação. Uma assinatura ou conexão de carteira não pode dar acesso a contas de terceiros.

## 9. Etapas de entrega e critérios de aceite

1. **Definição:** escolher segunda plataforma, instrumentos, estratégia, usuários iniciais e limites. Confirmar APIs e permissões.
2. **Painel somente leitura:** conectar carteira, mostrar posições reais e estado de atualização. Demonstração simulada deve estar rotulada.
3. **Execução em testes:** abrir, reconciliar e encerrar duas pernas; testar preenchimento parcial, rejeição, timeout, reconexão, reinício e revogação.
4. **Piloto pessoal limitado:** operar somente após autorização pertinente e validação dos limites definidos.
5. **Uso por terceiros:** adicionar isolamento de usuários, gestão segura de credenciais, histórico, recuperação operacional e suporte antes de abrir acesso.

Aceite mínimo: nenhuma ordem sem ativação explícita; nenhuma exposição duplicada após reinício; posição parcial identificada; pausa preserva monitoramento; reconciliação precede retomada; custos demonstráveis; dados antigos sinalizados; segredos ausentes dos logs; autorizações entre usuários isoladas. Validar a interface em desktop e celular, inclusive navegação por teclado e estados de falha.

## 10. Pendências e referências

Decisões pendentes: segunda plataforma, mercados iniciais, modalidade de arbitragem, limites financeiros, hospedagem, política de guarda de agentes, canais de alerta, modelo de cobrança e número de usuários do piloto. A arquitetura web é uma recomendação deste documento, sujeita à escolha do proprietário.

O repositório e este documento não constituem aprovação do TX Flow. Confirmar acesso e permissão expressa de automação antes de operar. Revalidar documentação e termos antes da implementação.

- [Agentes e autorização](https://docs.txflow.com/api/exchange/approveAgent)
- [Referência de API](https://docs.txflow.com/api/)
- [Limites](https://docs.txflow.com/api/rate-limits)
- [Builder Code](https://docs.txflow.com/getting-started/builder-code)
- [Candidatura](https://txflow.com/apply)
- [Termos](https://txflow.com/terms)

