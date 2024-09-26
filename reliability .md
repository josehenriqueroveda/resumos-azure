# Confiabilidade do Azure

A confiabilidade é composta por dois princípios: resiliência e disponibilidade. A meta de resiliência é evitar falhas e, se elas ainda ocorrerem, retornar seu aplicativo a um estado totalmente funcional. A meta de disponibilidade é fornecer acesso consistente ao seu aplicativo ou carga de trabalho. É importante planejar a confiabilidade proativa com base nos requisitos do aplicativo.

O Azure inclui serviços de confiabilidade integrados que você pode usar e gerenciar com base em suas necessidades de negócios. Seja uma única falha de nó de hardware, uma falha no nível do rack, uma interrupção do datacenter ou uma interrupção regional em grande escala, o Azure fornece soluções que aprimoram a confiabilidade. Por exemplo, os conjuntos de disponibilidade garantem que as máquinas virtuais implantadas no Azure sejam distribuídas entre vários nós de hardware isolados em um cluster. As zonas de disponibilidade protegem os aplicativos e dados dos clientes contra falhas de datacenter em vários locais físicos em uma região. As regiões e as zonas de disponibilidade são fundamentais para o design e a estratégia de resiliência do seu aplicativo e são discutidas mais detalhadamente adiante neste artigo.

A documentação de confiabilidade do Azure oferece diretrizes de confiabilidade para os serviços do Azure. Essas diretrizes incluem informações sobre o suporte à zona de disponibilidade, diretrizes de recuperação de desastre e disponibilidade de serviços.

Para obter diretrizes detalhadas de confiabilidade específicas do serviço, incluindo zonas de disponibilidade, recuperação de desastre ou alta disponibilidade, consulte Visão geral das diretrizes de confiabilidade específicas do serviço do Azure.


## Requisitos de confiabilidade

O nível necessário de confiabilidade para qualquer solução do Azure depende de várias considerações. O SLA de disponibilidade e latência e outros requisitos de negócios impulsionam as opções de arquitetura e o nível de resiliência e devem ser considerados em primeiro lugar. Os requisitos de disponibilidade variam de quanto tempo de inatividade é aceitável – e quanto custa para a sua empresa – até a quantidade de dinheiro e tempo que você pode investir de maneira realista para tornar um aplicativo altamente disponível.

A criação de sistemas de confiabilidade no Azure é uma responsabilidade compartilhada. A Microsoft é responsável pela confiabilidade da plataforma de nuvem, incluindo sua rede global e seus data centers. Os clientes e parceiros do Azure são responsáveis pela resiliência de seus aplicativos de nuvem, usando as melhores práticas de arquitetura com base nos requisitos de cada carga de trabalho. Embora o Azure se esforce continuamente pela maior resiliência possível no SLA para a plataforma de nuvem, você tem que definir suas próprias metas de SLA para cada carga de trabalho em sua solução. Um SLA possibilita avaliar se a arquitetura atende aos requisitos de negócios. À medida que você se esforça por percentuais mais altos de tempo de atividade garantido pelo SLA, o custo e a complexidade para alcançar esse nível de disponibilidade crescem. Um tempo de atividade de 99,99% se traduz em cerca de cinco minutos de tempo de inatividade total por mês. Vale a pena a complexidade e o custo para alcançar esse percentual? A resposta depende dos requisitos de negócios específicos. Enquanto decide os compromissos finais do SLA, entenda os SLAs da Microsoft com suporte. Cada serviço do Azure tem seu próprio SLA.

![](https://learn.microsoft.com/pt-br/azure/reliability/media/shared-responsibility.svg)

No modelo local tradicional, toda a responsabilidade de gerenciar o hardware, a computação, o armazenamento, a rede e o aplicativo, recai sobre você. Você deve planejar vários tipos de falhas e como lidar com elas criando uma estratégia de recuperação de desastre. Com o IaaS, o provedor de serviços de nuvem é responsável pela resiliência de infraestrutura principal, incluindo armazenamento, rede e computação. À medida que você passa de IaaS para PaaS e, em seguida, para SaaS, você descobrirá que é responsável por menos e o provedor de serviços de nuvem é responsável por mais.  

## Criando confiabilidade

Você precisa definir os requisitos de confiabilidade do aplicativo no início do planejamento. Se você souber quais aplicativos não precisam de 100% de disponibilidade alta durante determinados períodos de tempo, você poderá otimizar os custos durante esses períodos não críticos. Identifique os tipos de falhas que um aplicativo pode enfrentar, e os possíveis efeitos de cada falha. Um plano de recuperação deve abranger todos os serviços críticos, finalizando a estratégia de recuperação no componente individual e no nível geral do aplicativo. Projete sua estratégia de recuperação para se proteger contra falhas nos níveis zonais, regionais e do aplicativo. Execute testes do ambiente de aplicativo de ponta a ponta para medir a confiabilidade e a recuperação do aplicativo contra falhas inesperadas.

A lista de verificação a seguir aborda o escopo do planejamento de confiabilidade.

- Planejamento de confiabilidade
- Defina metas de disponibilidade e recuperação para atender aos requisitos de negócio.
- Projete os recursos de confiabilidade de seus aplicativos com base nos requisitos de disponibilidade.
- Alinhe aplicativos e plataformas de dados para atender aos seus requisitos de confiabilidade.
- Configure caminhos de conexão para promover a disponibilidade.
- Use zonas de disponibilidade e planejamento de recuperação de desastre quando aplicável a fim de melhorar a confiabilidade e otimizar os custos.
- Confirme se a arquitetura do seu aplicativo é resiliente a falhas.
- Saiba o que acontece se os requisitos de SLA não forem atendidos.
- Identifique possíveis pontos de falha no sistema; o design do aplicativo deve tolerar falhas de dependência implantando quebras de circuito.
- Crie aplicativos que operam até mesmo na ausência de suas dependências.

  ## RTO e RPO

  Duas métricas importantes a considerar são o Objetivo do Tempo de Recuperação e o Objetivo do Ponto de Recuperação, pois elas pertencem à recuperação de desastres.  Para obter mais informações sobre requisitos de design funcionais e não funcionais, consulte requisitos funcionais e não funcionais do Well-architected Framework.

- **Objetivo do Tempo de Recuperação (RTO)** é o tempo máximo aceitável que um aplicativo pode ficar indisponível após um incidente.

- **Objetivo do Ponto de Recuperação (RPO)** é a duração máxima de perda de dados aceitável durante um desastre.

RTO e RPO são os requisitos não funcionais de um sistema e devem ser determinados pelos requisitos de negócios. Para obter esses valores, é uma boa ideia conduzir uma avaliação de risco para compreender claramente o custo do tempo de inatividade ou da perda de dados.  

## Regiões e zonas de disponibilidade

Regiões e zonas de disponibilidade são uma grande parte da equação de confiabilidade. As regiões apresentam várias zonas de disponibilidade fisicamente separadas. Essas zonas de disponibilidade são conectadas por uma rede de alto desempenho com menos de 2 ms de latência entre zonas físicas. A baixa latência ajuda seus dados a permanecerem sincronizados e acessíveis quando as coisas dão errado. Você pode usar essa infraestrutura estrategicamente ao arquitetar aplicativos e infraestrutura de dados que replicam e entregam automaticamente serviços ininterruptos entre zonas e entre regiões.

Os serviços do Microsoft Azure dão suporte a zonas de disponibilidade e são habilitados para impulsionar suas operações de nuvem com alta disponibilidade ideal, ao mesmo tempo que dão suporte às suas necessidades de estratégia de continuidade de negócios e recuperação entre regiões.

Para o planejamento de recuperação de desastre, as regiões emparelhadas com outras regiões oferecem a replicação entre regiões e fornecem proteção replicando dados de forma assíncrona em outras regiões do Azure. Regiões sem par seguem diretrizes de residência de dados e oferecem alta disponibilidade com zonas de disponibilidade e armazenamento com redundância local ou com redundância de zona. Os clientes precisarão planejar sua recuperação de desastre entre regiões com base em suas necessidades de RTO/RPO.

Escolha a melhor região para suas necessidades com base nas considerações técnicas e regulatórias: recursos de serviço, residência de dados, requisitos de conformidade e latência; e comece a desenvolver sua estratégia de confiabilidade.

![](https://unascimento.wordpress.com/wp-content/uploads/2020/01/azureresilienceservices4.png)
