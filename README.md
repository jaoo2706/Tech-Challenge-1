# Tech Challenge — Fase 1: NPS Preditivo

> **FIAP | Pós-Tech — Ciência de Dados**

---

## Estrutura do Repositório

```
Tech-Challenge-1/
├── README.md                        ← Este arquivo (requisitos 1, 2 e reflexão sobre modelo)
├── data/
│   └── desafio_nps_fase_1.csv       ← Base de dados original
├── notebooks/
│   └── analises.ipynb               ← EDA + modelo preditivo (requisitos 3 e 4)
└── reports/
    └── storytelling.pptx            ← Apresentação gerencial
```

---

## Objetivo do Projeto

Uma empresa de e-commerce percebeu alta variabilidade no NPS entre seus clientes. Mesmo com indicadores operacionais aparentemente semelhantes, alguns clientes tornam-se promotores e outros, detratores. O objetivo deste projeto é **identificar quais fatores operacionais mais influenciam a satisfação do cliente** e propor como a empresa pode agir de forma proativa — antes mesmo da aplicação da pesquisa de NPS.

---

## Descrição da Base de Dados

A base contém **2.500 registros** de pedidos, com dados de logística, atendimento e perfil do cliente. Sem valores nulos.

| Variável | Descrição |
|---|---|
| `customer_id` | Identificador único do cliente |
| `order_id` | Identificador único do pedido |
| `customer_age` | Idade do cliente |
| `customer_region` | Região geográfica |
| `customer_tenure_months` | Tempo de relacionamento com a empresa (meses) |
| `order_value` | Valor total do pedido |
| `items_quantity` | Quantidade de itens |
| `discount_value` | Valor de desconto aplicado |
| `payment_installments` | Número de parcelas |
| `delivery_time_days` | Tempo total de entrega (dias) |
| `delivery_delay_days` | Dias de atraso na entrega |
| `freight_value` | Valor do frete |
| `delivery_attempts` | Tentativas de entrega |
| `customer_service_contacts` | Contatos com o atendimento |
| `resolution_time_days` | Tempo para resolução de problemas (dias) |
| `complaints_count` | Número de reclamações registradas |
| `repeat_purchase_30d` | Recompra em até 30 dias (0/1) |
| `csat_internal_score` | Score interno de satisfação |
| `nps_score` | **Nota NPS (0 a 10) — variável alvo** |

---

## Requisito 1 — Entendimento do Negócio

### Qual problema de negócio está sendo resolvido?

A empresa coleta o NPS **apenas após o encerramento da jornada de compra** — depois que o pedido foi entregue e qualquer problema já afetou o cliente. Isso limita completamente a capacidade de agir de forma preventiva. O problema central é que **a empresa não consegue antecipar a insatisfação**: age no "apagar incêndio" em vez de evitar que ele aconteça.

A solução passa por entender quais variáveis operacionais estão mais associadas à satisfação, para que áreas como logística e atendimento possam ser alertadas **durante** a jornada — antes do cliente virar detrator.

### Por que o NPS é importante para um e-commerce?

O e-commerce é um mercado com baixíssima barreira de troca. O cliente tem dezenas de alternativas a um clique. O NPS importa porque:

- **Resume a percepção total da experiência** em uma única métrica comparável ao longo do tempo e com concorrentes.
- **Prediz comportamento futuro**: promotores compram mais, gastam mais e indicam a marca; detratores abandonam e reclamam publicamente.
- **Facilita priorização**: ao cruzar NPS com dados operacionais, a empresa descobre *onde* melhorar, não apenas *que* está mal.

No e-commerce nacional, onde o NPS médio do setor gira entre 30 e 50 pontos, uma empresa com NPS negativo está perdendo market share ativamente.

### Quais áreas se beneficiam desses insights?

| Área | Como se beneficia |
|---|---|
| **Logística** | Identificar limiares de atraso que destroem o NPS; ajustar SLAs com transportadoras |
| **Atendimento ao Cliente** | Reduzir recontatos; priorizar casos com risco de insatisfação |
| **Produto / Tecnologia** | Melhorar rastreamento, notificações e pós-venda |
| **Pricing / Comercial** | Entender se frete elevado afeta a percepção de valor |
| **Estratégia** | Basear decisões em dados reais de experiência, não em suposições |

### Como o NPS impacta o negócio?

**Recompra:** Promotores recompram mais. Na nossa base, 100% dos promotores realizaram recompra em 30 dias, contra 0% dos detratores — confirmando que NPS e receita recorrente estão diretamente ligados.

**Boca a boca:** Detratores não ficam em silêncio. Eles reclamam no Reclame Aqui, Google, redes sociais e para conhecidos. Um único detrator pode afastar múltiplos clientes potenciais. Promotores fazem o oposto: indicam organicamente, reduzindo o custo de aquisição (CAC).

**Market share:** Em e-commerce, a experiência *é* o produto. Empresas que entregam NPS consistentemente alto constroem uma vantagem difícil de copiar — fidelidade, menor churn e crescimento orgânico. A médio prazo, ganham market share de concorrentes que negligenciam a experiência.

### Indicadores de mercado que complementariam a análise

- **Benchmark de NPS do setor**: e-commerces de grande porte no Brasil têm NPS entre 30-60 pontos — posicionar a empresa nesse espectro daria urgência real à melhoria.
- **SLA logístico de mercado**: prazo médio dos grandes marketplaces (ex.: promessa de 1-3 dias úteis) como referência de expectativa do consumidor.
- **Taxa de reclamações no Reclame Aqui**: benchmark setorial de tempo de resposta e índice de resolução.
- **Churn rate**: correlacionado com NPS; ajudaria a quantificar financeiramente o impacto de cada ponto de NPS perdido.
- **Net Revenue Retention (NRR)**: mede se clientes estão expandindo ou reduzindo gastos — fortemente ligado à satisfação.

---

## Requisito 2 — Definição da Target

### Qual variável representa a satisfação do cliente?

A variável `nps_score`, que varia de **0 a 10**, coletada por pesquisa após a experiência de compra. A partir dela, os clientes são segmentados em:

| Faixa | Categoria |
|---|---|
| 0 a 6 | Detratores |
| 7 e 8 | Neutros |
| 9 e 10 | Promotores |

Na base analisada: **74% detratores, 18% neutros, 8% promotores** — proporção que sinaliza problema operacional sistêmico.

### Por que ela foi escolhida?

O NPS é a métrica de satisfação mais padronizada e comparável do mercado. Diferente de avaliações de estrelas (que variam por plataforma), o NPS tem metodologia única e amplamente adotada, permitindo comparar a empresa com concorrentes e acompanhar evolução temporal. Ela captura a *intenção de recomendação* — proxy forte de comportamento futuro real.

### Em que momento da jornada essa informação é coletada?

O NPS é coletado **após o encerramento completo da jornada**: pedido entregue e eventuais problemas resolvidos. Isso o torna uma métrica **reativa** — o cliente já viveu toda a experiência antes de responder. É exatamente por isso que a empresa precisa de um modelo preditivo: para antecipar o resultado *durante* a jornada, não depois.

### Existe algum risco de usar essa variável de forma inadequada?

Sim. Os principais riscos são:

1. **Viés de resposta**: clientes com experiências extremas (muito boa ou muito ruim) respondem mais — o que pode distorcer a média.

2. **NPS não explica a causa**: ele mede o resultado, não o motivo. Sem cruzar com dados operacionais, o NPS sozinho não indica o que melhorar.

3. **Data leakage no modelo preditivo** (risco técnico crítico): algumas variáveis da base são coletadas junto com ou **após** o NPS. Usá-las como features de um modelo preditivo cria **vazamento de dados** — o modelo aprende com informações que não estariam disponíveis na hora da previsão, gerando performance inflada e inutilizável na prática. Detalhado no Requisito 4.

4. **Limitação preventiva**: como é coletado ao final, o NPS isolado não permite intervir a tempo. Daí a necessidade de transformar dados operacionais em sinais antecipados de insatisfação.

---

## Metodologia

### Análise Exploratória (EDA)
- Estatísticas descritivas e verificação de qualidade da base
- Distribuição de clientes por categoria NPS
- Correlação entre variáveis numéricas e NPS
- Comparação de métricas por categoria (Detrator / Neutro / Promotor)
- Análise de pontos de ruptura por faixas de atraso e contatos

### Modelo Preditivo
- Avaliação criteriosa de data leakage (veja Requisito 4 no notebook)
- Features selecionadas: variáveis disponíveis antes da coleta do NPS
- Algoritmo: RandomForestRegressor (300 estimadores)
- Separação: 80% treino / 20% teste
- Métrica: R²
- Avaliação de importância via Permutation Importance

---

## Requisito 3 — Análise Exploratória (resumo executivo)

> Análise completa com código e gráficos em `notebooks/analises.ipynb`.

### Fatores mais críticos para a satisfação

Três fatores se destacam com clareza na correlação com NPS:

1. **Atraso na entrega** (`delivery_delay_days`): correlação -0,60 — o fator mais relevante.
2. **Volume de reclamações** (`complaints_count`): correlação -0,50.
3. **Contatos com atendimento** (`customer_service_contacts`): correlação -0,35.

### O que mais gera detratores?

Detratores têm, em média:
- 2,53 dias de atraso (vs. 0,76 dos promotores)
- 4,62 reclamações (vs. 2,39 dos promotores)
- 1,69 contatos com suporte (vs. 0,78 dos promotores)
- 5,79 dias para resolução (vs. 4,10 dos promotores)

### Pontos de ruptura na experiência

**Atraso na entrega:**

| Faixa | NPS médio |
|---|---|
| Sem atraso | 6,86 |
| 1-2 dias | 5,05 |
| 3-5 dias | 2,89 |
| 6-10 dias | 0,81 |

A partir de 3 dias de atraso, o NPS já cai para a zona de detrator.

**Contatos com atendimento:**

| Contatos | NPS médio |
|---|---|
| 0 | 5,54 |
| 1 | 4,66 |
| 2 | 4,12 |
| 3-4 | 3,04 |
| 5+ | 1,93 |

### Perfil dos clientes por NPS

**Promotores**: receberam no prazo, não acionaram o suporte, tiveram resolução rápida quando necessário. Jornada simples e sem fricção. Todos recompraram em 30 dias.

**Detratores**: sofreram atrasos, reclamaram, precisaram contatar o suporte múltiplas vezes, e a resolução foi demorada. São **74% da base**.

**O que NÃO explica o NPS**: idade, região, valor do pedido, número de itens e forma de pagamento têm correlação desprezível (< 0,05). O NPS é explicado pela **qualidade da execução operacional**, não pelo perfil do cliente.

---

## Requisito 4 — Reflexão sobre Modelo Preditivo

> Implementação completa em `notebooks/analises.ipynb`.

### Estratégia adotada

**Problema como regressão**: mantemos `nps_score` como variável contínua (0-10). Isso preserva granularidade — saber se um cliente está em risco de NPS 2 ou NPS 5 tem implicação operacional diferente.

### Atenção crítica: data leakage

Antes de qualquer modelagem, avaliamos se cada variável estaria disponível **no momento em que a previsão seria feita** — ao final da entrega, antes do NPS ser coletado:

| Variável | Disponível antes do NPS? | Decisão |
|---|---|---|
| `delivery_delay_days`, `delivery_time_days`, `delivery_attempts` | ✅ Sim — dados da entrega | Incluir |
| `freight_value`, `order_value`, `items_quantity`, etc. | ✅ Sim — dados do pedido | Incluir |
| `customer_age`, `customer_region`, `customer_tenure_months` | ✅ Sim — perfil do cliente | Incluir |
| `customer_service_contacts`, `resolution_time_days` | ⚠️ Parcialmente — podem ocorrer durante ou após a jornada | Incluir com ressalva |
| `complaints_count` | ❌ Não — reclamação é **consequência** do problema, não causa. Usar criaria leakage | **Excluir** |
| `csat_internal_score` | ❌ Não — outra métrica de satisfação, simultânea ao NPS | **Excluir** |
| `repeat_purchase_30d` | ❌ Não — ocorre 30 dias *após* o pedido | **Excluir** |

### Resultados dos modelos

| Configuração | R² | Observação |
|---|---|---|
| Só features seguras (sem leakage) | **0,35** | Modelo honesto e deployável |
| + contacts e resolution_time | **0,52** | Variáveis discutíveis, mas defensáveis |
| Com tudo (inclui leakage) | **0,62** | Inflado — inútil na prática |

O principal driver é `delivery_delay_days` — com 76% da importância no modelo sem leakage. Isso confirma que **atraso na entrega é o coração do problema**.

### Como seria usado na prática

Ao final de cada entrega (antes do envio da pesquisa), o modelo receberia os dados operacionais e geraria uma **previsão de NPS**. Casos com previsão baixa seriam sinalizados para ação imediata: contato proativo, oferta de compensação ou alerta para a equipe de logística. A empresa passaria de **reativa para preventiva**.

---

## Como Reproduzir os Resultados

### Pré-requisitos

```bash
pip install pandas matplotlib scikit-learn
```

### Passos

1. Clone o repositório
2. Coloque o arquivo CSV em `data/desafio_nps_fase_1.csv`
3. Abra `notebooks/analises.ipynb`
4. Execute todas as células em ordem

> Desenvolvido com Python 3.10.
