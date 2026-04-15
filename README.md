# Tech Challenge - Fase 1
### Case: NPS Preditivo  

---

## Requisito 1: **Entendimento do negócio**

### 1. Qual problema de negócio está sendo resolvido?

O principal problema aqui é que a empresa só consegue entender se o cliente ficou satisfeito depois que toda a jornada já acabou, através do NPS. Isso acaba limitando bastante a atuação, porque qualquer problema que aconteceu já impactou o cliente.

Ou seja, hoje a empresa age mais no “apagar incêndio” do que em evitar que ele aconteça. Se teve atraso, problema no atendimento ou frustração com o produto, isso só vai aparecer depois, quando já não tem muito o que fazer.

Então o desafio é justamente tentar prever isso antes. A ideia é usar os dados da operação (entrega, atendimento, pedido, etc.) pra entender o que está levando um cliente a virar detrator ou promotor, e com isso agir antes da experiência ficar ruim.

---

### 2. Por que o NPS é importante para um e-commerce?

O NPS é importante porque mostra, de forma bem direta, como o cliente enxerga a empresa e se ele recomendaria ou não.

No e-commerce isso pesa ainda mais, porque o cliente tem várias opções e pode trocar de loja muito fácil. Às vezes, um atraso ou um frete caro já é suficiente pra ele não voltar mais.

Além disso, o NPS ajuda a juntar vários pontos da experiência em um único número, o que facilita acompanhar se a empresa está melhorando ou piorando ao longo do tempo. Também ajuda a entender onde estão os principais problemas.

---

### 3. Quais áreas poderiam se beneficiar desses insights?

#### Logística
A logística é uma das áreas que mais impactam o cliente. Atrasos, prazo mal definido ou frete caro influenciam direto na experiência. Com esses insights, dá pra ajustar melhor as promessas de entrega e melhorar a operação.

#### Atendimento ao cliente
Se a empresa conseguir identificar clientes que estão com risco de ficar insatisfeitos, o atendimento pode agir antes da reclamação acontecer. Isso ajuda a evitar problemas maiores e melhora a experiência.

#### Produto / Experiência digital
Problemas no site, dificuldade no checkout ou diferença entre o que o cliente espera e o que recebe também influenciam bastante. Esses dados ajudam a melhorar tanto o site quanto a apresentação dos produtos.

#### Pricing / Comercial
O preço e principalmente o frete têm um peso grande na decisão do cliente. Entender esse impacto ajuda a ajustar melhor as estratégias comerciais.

#### Estratégia / Negócio
No geral, esses insights ajudam a empresa a focar no que realmente importa pra experiência do cliente, ao invés de tomar decisão no “achismo”.

---

### 4. Como o NPS impacta o negócio?

#### Recompra
Clientes satisfeitos tendem a comprar de novo. Já clientes insatisfeitos dificilmente voltam. Então o NPS acaba tendo uma relação direta com retenção.

---

#### Boca a boca
O cliente que teve uma boa experiência costuma indicar a marca, enquanto quem teve uma experiência ruim geralmente compartilha isso com outras pessoas. No e-commerce, isso aparece muito em avaliações e redes sociais.

---

#### Market share em e-commerce
Empresas que entregam uma experiência melhor acabam conseguindo manter mais clientes e atrair novos, principalmente por indicação. Com o tempo, isso ajuda a ganhar espaço no mercado.

---

### Conclusão

O NPS não é só um número de satisfação. Ele ajuda a entender o que está funcionando (ou não) na experiência do cliente.

Se a empresa conseguir usar isso de forma mais antecipada, ela deixa de só reagir aos problemas e passa a evitá-los, o que impacta diretamente na retenção e no crescimento do negócio.

---

## Requisito 2: **Definição da Target**

### 1. Qual variável representa a satisfação do cliente?

A variável que representa a satisfação do cliente é o nps_score.

Ela vai de 0 a 10 e mostra o quanto o cliente ficou satisfeito com a experiência como um todo. É a forma mais direta de medir a percepção final do cliente sobre a empresa.

---

### 2. Por que ela foi escolhida?

O nps_score foi escolhido porque é uma métrica consolidada no mercado e representa bem o resultado final da experiência do cliente.

Além disso, ele permite segmentar os clientes de forma clara:
- 0 a 6 → detratores  
- 7 e 8 → neutros  
- 9 e 10 → promotores  

Isso facilita entender rapidamente quem teve uma boa experiência e quem teve problemas.

Por outro lado, é importante destacar que o NPS não explica sozinho o que causou essa satisfação ou insatisfação. Ele mostra o resultado final, mas não os motivos, o que reforça a necessidade de analisá-lo junto com dados operacionais.

---

### 3. Em que momento da jornada essa informação é coletada?

O NPS é coletado após o encerramento da jornada do cliente.

Ou seja, depois que:
- o pedido foi entregue  
- possíveis problemas foram resolvidos  
- o cliente já teve a experiência completa  

Isso faz com que ele seja uma métrica reativa, já que só é conhecida depois que tudo aconteceu.

---

### 4. Existe algum risco de usar essa variável de forma inadequada?

Sim, existem alguns pontos de atenção importantes.

#### Uso de dados que acontecem depois da experiência

Se forem utilizadas variáveis que só existem após o problema acontecer, o modelo pode acabar usando informações que não estariam disponíveis no momento da previsão.

Por exemplo:
- número de reclamações  
- tempo de resolução  

Esses dados ajudam a explicar o NPS, mas não necessariamente a prever antes da experiência terminar.

---

#### Viés de quem responde

Nem todos os clientes respondem o NPS.

Normalmente, quem responde são clientes com experiências muito boas ou muito ruins, o que pode gerar uma visão distorcida da base total de clientes.

---

#### NPS mostra o resultado, não a causa

O NPS indica o nível de satisfação, mas não explica diretamente o motivo.

Por isso, ele precisa ser analisado em conjunto com variáveis como entrega, atendimento e características do pedido para gerar insights acionáveis.

---

#### Limitação para ação preventiva

Como o NPS é coletado apenas no final da jornada, ele não permite que a empresa atue de forma antecipada.

Esse é justamente o principal problema de negócio: a empresa acaba reagindo depois, ao invés de evitar que a experiência seja ruim.

---

### Conclusão

O nps_score é uma boa variável para representar a satisfação do cliente, pois resume a percepção final da experiência em uma única métrica.

No entanto, por ser coletado apenas após a jornada, ele deve ser utilizado junto com dados operacionais para permitir análises mais completas e possibilitar ações preventivas.

---

## Requisito 3: **Análise Exploratória dos Dados (EDA)**

### 1. Quais fatores parecem mais críticos para a satisfação?

Para identificar os fatores mais críticos, foram utilizadas três abordagens complementares no notebook analises.ipynb: análise de correlação com o nps_score, comparação entre grupos de clientes (detratores, neutros e promotores) e avaliação de importância de variáveis por meio de um modelo preditivo.

Os resultados foram consistentes entre essas análises.

As variáveis que mais se destacaram foram:
- delivery_delay_days
- complaints_count
- customer_service_contacts
- resolution_time_days

Essas métricas apresentaram associação relevante com o NPS e diferenças claras entre os grupos analisados, conforme evidenciado nos gráficos e tabelas gerados no notebook.

Isso indica que problemas logísticos e dificuldades no atendimento estão entre os principais fatores relacionados à insatisfação do cliente.

---

### 2. O que mais gera detratores?

A partir das análises realizadas no analises.ipynb, os detratores apresentam padrões bem consistentes quando comparados aos promotores:

- Maior atraso na entrega  
- Maior número de reclamações  
- Mais contatos com o atendimento  
- Maior tempo de resolução de problemas  

Esses fatores aparecem tanto na análise descritiva quanto na avaliação do modelo, o que reforça a relação entre falhas operacionais e baixa satisfação.

Ou seja, o detrator normalmente não surge de forma aleatória, mas sim como consequência de uma jornada com atritos.

---

### 3. Existe algum “ponto de ruptura” na experiência do cliente?

A análise exploratória também indicou possíveis pontos de ruptura na experiência.

No caso do atraso na entrega, por exemplo, observou-se que o NPS tende a cair conforme aumentam os dias de atraso, o que sugere uma tolerância limitada por parte do cliente.

O mesmo comportamento foi observado em relação ao número de contatos com o atendimento. A partir de múltiplas interações, a experiência deixa de ser pontual e passa a ser percebida como problemática.

Esses padrões foram identificados a partir das análises por faixa realizadas no notebook, indicando limites operacionais relevantes.

---

### 4. Que tipo de cliente tende a ter NPS mais alto ou mais baixo?

Clientes com NPS mais alto (promotores) geralmente apresentam uma jornada mais simples:

- Recebem o pedido dentro do prazo  
- Não precisam acionar o atendimento  
- Não registram reclamações  
- Têm resolução rápida quando há algum problema  

Já os clientes com NPS mais baixo (detratores):

- Sofrem com atrasos na entrega  
- Precisam entrar em contato com o atendimento várias vezes  
- Têm problemas que demoram para ser resolvidos  
- Apresentam maior número de reclamações  

Também foram observadas variáveis com alta associação ao NPS, como repeat_purchase_30d e csat_internal_score. No entanto, essas métricas foram analisadas com cautela no notebook, pois podem representar consequência da satisfação ou estar muito próximas do próprio conceito de NPS.

---

### Conclusão

A análise exploratória realizada no notebook analises.ipynb mostra que a satisfação do cliente está diretamente ligada à qualidade da operação, principalmente nos processos de logística e atendimento.

As evidências foram consistentes entre diferentes abordagens analíticas, indicando que atraso na entrega, volume de reclamações, necessidade de suporte e tempo de resolução são fatores relevantes para explicar a variação do NPS.

Isso reforça que a empresa pode melhorar a satisfação não apenas medindo o resultado final, mas atuando diretamente nos processos que influenciam a experiência ao longo da jornada.