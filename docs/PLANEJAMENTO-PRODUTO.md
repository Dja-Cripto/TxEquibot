# TxEquibot — planejamento de produto e candidatura

Pesquisa: 23/10/2026. Status: proposta, sem integração real validada.

> **Atualização (23/10/2026):** o foco do produto voltou a ser o ciclo delta neutro entre duas plataformas, com o TX Flow como plataforma principal, um gate de edge mínimo, taxa de Builder Code visível e testnet primeiro. Este documento fica como registro da pesquisa comparativa e do raciocínio sobre avaliação; onde as seções 1, 5 e 9 descreverem um MVP de uma plataforma só, vale o [README](../README.md) e os documentos em inglês. O host da mainnet do TX Flow está confirmado na documentação (`https://rpc.txflow.com`), mas o acesso de escrita continua sujeito a aprovação.

## 1. Decisão recomendada

Construir uma aplicação web focada no TX Flow para configurar, avaliar e acompanhar bots de trading. Jornada central: definir regras → simular → revisar custos e riscos → autorizar execução → comparar resultado observado com a configuração original.

Público inicial: usuários individuais do TX Flow que desejam automação configurável e entendimento do desempenho. Desenvolvedor: solo builder. Objetivo futuro: disponibilizar o site a outras pessoas, com piloto pequeno antes de acesso amplo.

Posicionamento: **TxEquibot — configure, avalie e acompanhe seus bots no TX Flow.** Não prometer retorno, aprovação quase certa, preferência oficial por uma categoria ou inovação exclusiva.

## 2. Evidências e limites

Na captura do ticket fornecida pelo usuário, o suporte confirma que desenvolvedores individuais e projetos na fase de ideia podem se candidatar, sem empresa estabelecida ou protótipo funcional. Seleção e acesso continuam sujeitos à análise da engenharia. Isso confirma elegibilidade, não aprovação do TxEquibot.

O formulário oferece categorias de trading, gestão de portfólio e analytics. O programa de Builder Code documenta bots e aplicações que encaminham operações de usuários. Esse é o alinhamento publicado que fundamenta a proposta; não foi encontrada pontuação pública de seleção ou taxa de aprovação por categoria. [Candidatura](https://txflow.com/apply) · [Builder Code](https://docs.txflow.com/getting-started/builder-code)

A documentação distingue mainnet restrita a contas autorizadas e testnet sem candidatura. Logo, o acesso real depende da seleção, mas planejamento, protótipo visual, simulação e exploração dos recursos de teste não precisam aguardar a liberação da mainnet. [Exchange API](https://docs.txflow.com/api/exchange)

## 3. Pesquisa comparativa

Referências escolhidas pela relevância funcional e documentação pública. Não se trata de ranking dos maiores: não foi feita validação independente de participação de mercado, usuários ou volume.

| Referência | O que a fonte oficial documenta | Lição para o TxEquibot |
|---|---|---|
| MyLiquidBot | Conexão TX Flow por agente, bots, acompanhamento e ferramentas de backtest | Reduzir etapas de configuração e mostrar claramente autorização e estado do bot |
| 3Commas | Configuração de DCA e backtesting com período e estatísticas | Avaliar uma configuração antes de executar e manter um registro reproduzível |
| Cryptohopper | Teste histórico e paper trading como formas distintas de avaliação | Separar simulação no passado, simulação acompanhando o mercado e operação real |
| Hummingbot | Configuração, métricas e implantação de estratégias; o Dashboard antigo está descontinuado em favor de Condor | Separar interface, estratégia e executor; verificar manutenção antes de escolher componentes |

Fontes: [MyLiquidBot](https://myliquidbot.com/docs?lang=en), [3Commas](https://help.3commas.io/en/articles/4829733-dca-bots-backtesting), [Cryptohopper](https://www.cryptohopper.com/blog/how-does-backtesting-work-11207), [Hummingbot Dashboard](https://hummingbot.org/dashboard/), [Hummingbot backtesting](https://hummingbot.org/dashboard/backtest/).

MyLiquidBot divulga suporte a TX Flow; não foi comprovada parceria pública ou autorização individual concedida pelo TX Flow. Não apresentá-lo na candidatura como cliente oficialmente aprovado com base apenas no site dele.

## 4. Problema e proposta de valor

Hipótese de problema a validar com usuários: configurar um bot não esclarece quanto ele pode consumir em custos, quanto pode perder numa sequência adversa e se o resultado real corresponde à simulação.

Proposta: cada bot terá uma ficha de estratégia versionada, uma avaliação com premissas visíveis e uma trilha de execução compreensível. O usuário verá resultado líquido, exposição, margem e motivo de cada entrada, saída ou pausa.

Esses recursos existem no mercado em diferentes formatos. Nosso foco é implementá-los de maneira coesa para TX Flow, com escopo pequeno e transparência. A diferenciação é uma hipótese de experiência de uso, não uma superioridade já demonstrada.

Benefícios potenciais para TX Flow, como inferência: facilitar adoção por usuários, encaminhar operações legítimas por integração suportada e fornecer feedback técnico estruturado. Não prometer volume, liquidez ou crescimento ainda não medidos. Um bot taker não deve ser apresentado como provedor de liquidez.

## 5. MVP para um desenvolvedor individual

### Bot inicial: execução por regras e tempo

Uma única família de estratégia: entrada manualmente configurada ou condicionada a preço, posição limitada, saída por regra de preço ou duração e controle de repetição. Configurar tamanho, direção, prazo máximo e limites antes de ativar. A seleção de ativos e parâmetros ainda depende de validação.

O temporizador organiza execução; não cria uma vantagem econômica. Operar apenas no TX Flow é direcional, não delta neutro. O modo protegido entre duas plataformas será identificado separadamente quando implementado.

### Avaliação inicial

Começar com simulação e paper trading explicitamente identificados. Acrescentar backtest histórico somente para mercados e períodos com dados suficientes e premissas compatíveis com a estratégia. Sem histórico de qualidade, mostrar a limitação em vez de inventar resultados.

Relatório: PnL líquido, maior queda do patrimônio, taxas, funding observado quando disponível, quantidade de operações, exposição máxima, duração média e interrupções. Comparar configurações no mesmo período e com o mesmo capital. Não produzir uma nota de aprovação ou recomendação de investimento disfarçada.

### Painel

Telas: Meus bots, Criar bot, Avaliação, Operações e Conexão. Visual profissional, responsivo, poucos indicadores prioritários, linguagem direta e diferença visível entre simulado, testnet e real. Pausar novas entradas e encerrar posição são controles distintos.

### Fora da primeira entrega

Marketplace, copy trading, martingale, dezenas de estratégias, agente de IA autônomo, suporte amplo a exchanges, aplicativo desktop e gestão de saques. Expansão delta neutra permanece no roadmap, sem ser dependência do MVP apresentado.

## 6. Como avaliar sem produzir resultados enganosos

- Guardar versão da estratégia, parâmetros, fonte, intervalo, granularidade e premissas de custos.
- Utilizar apenas dados disponíveis no instante de cada decisão; evitar informação futura.
- Separar período de ajuste e período de avaliação; registrar todas as versões relevantes, não apenas a melhor.
- Modelar spread, taxas, funding e slippage conforme a disponibilidade. Evidenciar custos estimados e dados ausentes.
- Em candles que atingem dois gatilhos, aplicar regra conservadora e divulgar a ambiguidade; não presumir preenchimento garantido de ordens limitadas.
- Nunca interpretar fills de testnet como prova de liquidez ou desempenho da mainnet.
- Na operação real, reconciliar fills, saldo, posição e taxas. Não descontar slippage duas vezes quando já estiver refletido no preço executado.
- Mostrar tamanho da amostra e períodos de dados ausentes. Resultado histórico não é previsão.

## 7. Arquitetura proposta

Interface web → serviço autenticado → estratégia versionada → executor persistente → adaptador TX Flow. Banco armazena configurações, intenções, ordens, fills e métricas. Simulador usa o mesmo contrato de estratégia, com ambiente e modelo de execução separados.

Autorização de carteira e agente são etapas explícitas. Credenciais delegadas protegidas e isoladas por usuário; chave principal nunca enviada ao servidor. Implementar revogação, limites, auditoria e recuperação de reinícios antes de abrir a terceiros.

API prevista: metadados, preços/livro, posições/margem, ordens/fills, funding e agente. Preferir streams e cache, com controle agregado por IP e reconciliação após interrupções. Detalhes disponíveis no [kit de integração](../integracoes/README.md).

## 8. Plano de entrega por evidências

| Fase | Entrega | Critério para avançar |
|---|---|---|
| Candidatura | README público, proposta, jornada e escopo | Informações coerentes e experiência descrita sem exageros |
| Demonstração | Telas e simulador com dados identificados | Usuário entende configurar, avaliar e parar o bot |
| Integração em teste | Consultas, autorização e ciclo de ordem | Recupera rejeição, timeout, revogação e reinício sem duplicar exposição |
| Piloto real autorizado | Bot inicial com limites, histórico e comparação | Fills reconciliados, custos auditáveis, controle de acesso e encerramento verificados |
| Pequeno grupo convidado | Contas isoladas, suporte e observabilidade | Nenhum acesso cruzado, incidentes rastreáveis e recuperação validada |
| Expansão | Novas estratégias e delta neutro | Evidência de demanda e execução confiável do MVP |

Sem prazo fechado nesta fase: dependências de API, disponibilidade de dados e tempo do desenvolvedor ainda precisam ser medidos. Não confundir roadmap com compromisso de entrega já financiado.

## 9. Preservação da ideia de ciclos delta neutros

Na expansão, suportar as duas pernas e duração configurável, incluindo 5 ou 12 horas. Contar após confirmação do hedge; antecipar saída por risco; encerrar e reconciliar ambas antes de repetir. Hibachi é uma candidata já estudada, sem limitar o posicionamento do produto a ela. Reutilizar [CICLOS.md](../integracoes/CICLOS.md) após validar os dois conectores.

## 10. Candidatura recomendada

Categoria principal: Trading Bot. Complementares, se o formulário permitir: Analytics / Dashboard e Portfolio Management. Equipe: Solo Builder se continuar sendo uma pessoa. Estágio: Idea Stage enquanto houver apenas documentação; Prototype após existir protótipo real. Não marcar AI Agent ou Market Making apenas para parecer mais atrativo.

Solicitar acesso para desenvolver uma aplicação web de configuração, avaliação e execução de bots para usuários TX Flow. Explicar claramente que a primeira versão terá uma família de estratégia e um piloto limitado.

O projeto anterior Hibachi pode demonstrar experiência com código de integração e painel local, sem afirmar lançamento público ou funcionamento atual. Número esperado de usuários e requisições devem ser estimados a partir do piloto, sem inventar base instalada.

Modelo comercial em estudo: plano de software ou Builder Code com aprovação explícita das taxas. Não definir percentuais antes de validar custos, experiência e condições aplicáveis.

## 11. Hipótese de consumo e métricas

Proposta de planejamento, não previsão confirmada: começar com um usuário interno e depois 3–5 convidados. Descoberta de mercados compartilhada, streams reaproveitados e reconciliação limitada. Uma consulta por minuto por conta já equivale a 1.440 consultas/dia; com cinco contas são 7.200 antes de ordens e outras leituras. Portanto, a categoria de uso da API depende do desenho final, não apenas de poucos usuários.

Medir ativação, conclusão de simulação, falhas de ordem, diferença de resultado estimado/real, idade dos dados, tempo de recuperação e retorno dos pilotos. Estabelecer metas após baseline; não anunciar números inventados como resultados.

## 12. O que torna a proposta defensável

Há alinhamento com os usos documentados, problema concreto, escopo solo viável e fases verificáveis. Isso melhora a clareza da avaliação; não revela os critérios internos do TX Flow nem garante seleção. Entregar uma boa proposta é o objetivo sob nosso controle.
