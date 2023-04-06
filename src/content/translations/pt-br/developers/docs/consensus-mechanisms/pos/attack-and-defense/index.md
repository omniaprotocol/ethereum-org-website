---
title: Ataque e defesa da prova de participação do Ethereum
description: Aprenda sobre os vetores de ataque conhecidos na prova de participação do Ethereum e como eles são defendidos.
lang: pt-br
---

Ladrões e sabotadores estão constantemente buscando oportunidades para atacar o software cliente do Ethereum. Esta página descreve os vetores de ataque conhecidos na camada de consenso do Ethereum e mostra como esses ataques podem ser defendidos. As informações nesta página são adaptadas de uma [versão mais longa do formulário](https://mirror.xyz/jmcook.eth/YqHargbVWVNRQqQpVpzrqEQ8IqwNUJDIpwRP7SS5FXs).

## Pré-requisitos {#prerequisites}

São necessários alguns conhecimentos básicos de [prova de participação](/developers/docs/consensus-mechanisms/pos/). Além disso, será útil ter um entendimento básico da [camada de incentivo](/docs/consensus-mechanisms/pos/rewards-and-penalties) do Ethereum e do algoritmo de escolha de fork, [LMD-GHOST](/docs/consensus-mechanisms/pos/gasper).

## O que os invasores querem? {#what-do-attackers-want}

Um equívoco comum é achar que um invasor bem-sucedido pode gerar um novo ether ou drenar ethers de contas arbitrárias. Nenhum desses dois é possível, pois todas as transações são executadas por todos os clientes de execução na rede. Eles devem satisfazer condições básicas de validade (por exemplo, transações são assinadas pela chave privada do remetente, o remetente tem saldo suficiente, etc.) ou então eles simplesmente se revertem. Há três classes de resultado que um invasor pode visar realistamente: reorgs, dupla finalidade ou atraso de finalidade.

Um **“reorg”** é uma reembaralhamento de blocos em uma nova ordem, talvez com alguma adição ou subtração de blocos na cadeia padrão. Uma reorganização maliciosa pode garantir que blocos específicos sejam incluídos ou excluídos, permitindo gastos duplos ou extração de valores ao executar transações front-running e back-running (MEV). As reorgs também podem ser usadas para evitar que certas transações sejam incluídas na cadeia padrão, o que é uma espécie de censura. A forma mais extrema de reorg é a “reversão da finalidade”, que remove ou substitui blocos que foram previamente finalizados. Isso só é possível se mais de 1/3 do ether total em stake for destruído pelo invasor — esta garantia é conhecida como “finalidade econômica” — falaremos mais sobre isso mais tarde.

**A finalidade dupla** é a condição improvável, mas severa, na qual dois forks são capazes de finalizar simultaneamente, criando uma cisão permanente na cadeia. Isso é teoricamente possível para um invasor que esteja disposto a arriscar 34% do total do ether em stake. A comunidade seria forçada a coordenar fora da cadeira e chegar a um acordo sobre qual cadeia seguir, o que exigiria força na camada social.

Um ataque de **atraso de finalidade** impede que a rede chegue às condições necessárias para finalizar as seções da cadeia. Sem finalidade, é difícil confiar em aplicativos financeiros construídos em cima do Ethereum. O objetivo de um ataque de atraso de finalidade é basicamente perturbar o Ethereum, em vez de lucrar diretamente com ele, a menos que o invasor tenha alguma posição vendida estratégica.

Um ataque à camada social poderia visar minar a confiança pública no Ethereum, desvalorizar o ether, reduzir a adoção ou enfraquecer a comunidade Ethereum para tornar a coordenação fora de banda mais difícil.

Tendo estabelecido por que adversários atacariam o Ethereum, as seções a seguir examinam _como_ eles o fariam.

## Métodos de ataque {#methods-of-attack}

### Ataques na Camada 0 {#layer-0}

Em primeiro lugar, os indivíduos que não participam ativamente no Ethereum (executando o software cliente) podem atacar visando a camada social (Camada 0). A Camada 0 é a fundação sobre a qual o Ethereum é construído, e, como tal, representa uma superfície potencial sujeita a ataques com consequências que se propagam pelo resto da pilha. Alguns exemplos podem incluir:

- Uma campanha de desinformação poderia prejudicar a confiança que a comunidade tem no roteiro, equipes de desenvolvedores, aplicativos do Ethereum, etc. Isso poderia então diminuir o número de indivíduos dispostos a participar protegendo a rede, degradando tanto a descentralização quanto a segurança criptoeconômica.
- Ataques direcionados e/ou intimidação voltados para a comunidade de desenvolvedores. Isso pode levar à saída voluntária de desenvolvedores e desacelerar o progresso do Ethereum.

- Regulamentação excessivamente zelosa também poderia ser considerada um ataque à Camada 0, uma vez que poderia desincentivar rapidamente a participação e a adoção.
- Infiltração de atores experientes, mas maliciosos, na comunidade de desenvolvedores, cujo objetivo é atrasar o progresso dando importância demais a questões simples, atrasando decisões-chave, criando spam, etc.
- Subornos a atores-chave do ecossistema Ethereum para influenciar a tomada de decisões.

O que torna estes ataques particularmente perigosos é que, em muitos casos, é necessário muito pouco capital ou conhecimentos técnicos. Um ataque à Camada 0 poderia ser um multiplicador em um ataque criptoeconômico. Por exemplo, se a censura ou a reversão da finalidade fossem alcançadas por uma parte interessada majoritária maliciosa, minar a camada social poderá tornar mais difícil coordenar uma resposta comunitária fora da banda.

Defender-se contra ataques à Camada 0 provavelmente não é uma tarefa simples, mas alguns princípios básicos podem ser estabelecidos. Uma delas é manter um sinal global alto de relação de ruído para informações públicas sobre o Ethereum, criado e propagado por membros honestos da comunidade por meio de blogs, servidores discord, especificações anotadas, livros, podcasts e Youtube. Aqui no ethereum.org, nos esforçamos para manter informações precisas e traduzi-las para o maior número de idiomas possível. Inundar um espaço com informações de alta qualidade e memes é uma defesa eficaz contra a desinformação.

Outro reforço importante contra os ataques às camadas sociais é uma declaração clara de missão e um protocolo de governança. O Ethereum se posicionou como o campeão de descentralização e segurança entre a camada 1 de contrato inteligente, enquanto também tem um elevado valor de escalabilidade e sustentabilidade. Independentemente dos desacordos que surgem na comunidade Ethereum, esses princípios fundamentais são minimamente comprometidos. A avaliação de uma narrativa contra esses princípios fundamentais e a análise destes por meio de sucessivas revisões no processo de EIP (Proposta de Melhoria Ethereum), poderá ajudar a comunidade a distinguir os bons dos maus atores e limitar o campo de influência de atores maliciosos na direção futura do Ethereum.

Por fim, é fundamental que a comunidade Ethereum permaneça aberta e receptiva a todos os participantes. Uma comunidade com guardiões e exclusividade é uma comunidade especialmente vulnerável a ataques sociais, pois é fácil construir narrativas que façam a segregação entre “nós e eles”. A criação de tribos e os exageros tóxicos prejudicam a comunidade e desgastam a segurança da camada 0. Os Ethereanos com um interesse manifesto na segurança da rede devem avaliar sua conduta online e presencial como contribuidores diretos para a segurança da Camada 0 do Ethereum.

### Atacando o protocolo {#attacking-the-protocol}

Qualquer um pode executar o software do cliente Ethereum. Para adicionar um validador a um cliente, um usuário precisa depositar 32 ethers em stake no contrato de depósito. Um validador permite que um usuário participe ativamente da segurança de rede Ethereum, propondo e atestando novos blocos. Os validadores agora têm voz ativa para influenciar o conteúdo futuro da blockchain. Eles podem fazer isso de forma honesta e, assim, aumentar seus ethers por meio de recompensas, ou podem tentar manipular o processo em benefício próprio, arriscando seu stake. Uma maneira de organizar um ataque é acumular uma maior proporção do stake total e, em seguida, usar isso para superar os votos dos validadores honestos. Quanto maior a proporção do stake controlado pelo atacante, maior será o seu poder de voto, especialmente em certos marcos econômicos que exploraremos mais tarde. No entanto, a maioria dos invasores não conseguirá acumular ethers suficientes para atacar dessa forma, portanto, eles têm de utilizar técnicas sutis para manipular a maioria honesta a agir de certa maneira.

Essencialmente, todos os ataques com pouco stake são variações sutis de dois tipos de mau comportamento: subatividade (sem conseguir atestar/propor ou fazendo-o tardiamente) ou superatividade (propondo/atestando muitas vezes em um slot). Nas suas formas mais simples essas ações são facilmente manipuladas pelo algoritmo de escolha de fork e camada de incentivo, mas existem maneiras mais inteligentes de manipular o sistema em benefício de um invasor.

### Ataques usando pequenas quantidades de ETH {#attacks-by-small-stakeholders}

#### reorgs {#reorgs}

Vários artigos descreveram ataques no Ethereum que obtêm reorgs ou atraso de finalidade com apenas uma pequena proporção do total de ethers em stake. Esses ataques geralmente dependem de que o atacante retenha algumas informações de outros validadores e, em seguida, divulgue-as de maneira sutil e/ou em algum momento oportuno. Eles geralmente visam deslocar algum(ns) bloco(s) honesto(s) da cadeia padrão. [Neuder et al 2020](https://arxiv.org/pdf/2102.02247.pdf) mostrou como um validador invasor pode criar e atestar um bloco (`B`) para um determinado slot `n+1` mas evita propagá-lo para outros nós da rede. Em vez disso, eles mantêm o bloco atestado até o próximo slot `n+2`. Um validador honesto propõe um bloco (`C`) para o slot `n+2`. Quase simultaneamente, o invasor pode liberar seu bloco retido (`B`) e suas atestações retidos para isso, e também atestar `B` como a cabeça da cadeia com seus votos no slot `n+2`, efetivamente negando a existência de um bloco honesto `C`. Quando o bloco honesto `D` é lançado, o algoritmo de escolha de fork vê `D` construir em cima de `B` como mais pesado do que `D` construindo em `C`. O invasor consegue então remover o bloco honesto `C` no slot `n+2` da cadeia padrão usando uma reorganização anterior de 1 bloco. [Um invasor com 34%](https://www.youtube.com/watch?v=6vzXwwk12ZE) do stake tem uma grande chance de sucesso nesse ataque, conforme explicado [nesta nota](https://notes.ethereum.org/plgVdz-ORe-fGjK06BZ_3A#Fork-choice-by-block-slot-pair). Em teoria, porém, esse ataque poderia ser tentado com stakes menores. [Neuder et al 2020](https://arxiv.org/pdf/2102.02247.pdf) descreveu esse ataque funcionando com um stake de 30%, que mais tarde revelou-se viável com [2% do stake total](https://arxiv.org/pdf/2009.04987.pdf) e depois novamente para um [único validador](https://arxiv.org/abs/2110.10086#) usando técnicas de balanceamento que iremos examinar na próxima seção.

![reorganização anterior](reorg-schematic.png)

Um diagrama conceitual do ataque de reorganização de um bloco descrito acima (adaptado de https://notes.ethereum.org/plgVdz-ORe-fGjK06BZ_3A#Fork-choice-by-block-slot-pair)

Um ataque mais sofisticado pode dividir o conjunto do validador honesto em grupos discretos contendo visões diferentes da cabeça da cadeia. Isso é conhecido como um **ataque de balanceamento**. O invasor espera pela sua oportunidade de propor um bloco e, quando ela chega, engana e propõe dois. Ele envia um bloco para metade do conjunto do validador honesto e o outro bloco para a outra metade. O erro seria detectado pelo algoritmo de escolha de fork e o proponente de blocos seria reduzido e removido pela rede, mas os dois blocos ainda existiriam e teriam cerca de metade do conjunto validador atestando cada fork. Enquanto isso, os demais validadores maliciosos retêm suas atestações. Em seguida, ao liberar seletivamente as atestações favorecendo um ou outro fork para apenas uma quantidade de validadores suficiente enquanto o algoritmo de escolha de fork está em execução, eles fazem pender o peso acumulado das atestações a favor de um ou outro fork. Isso pode continuar indefinidamente, com os validadores invasores mantendo uma divisão igual de validadores entre os dois forks. Como nenhum dos forks pode atrair uma supermaioria de 2/3, a Beacon Chain não consegue finalizar.

Os **ataques de salto** são semelhantes. Os votos são novamente retidos pelos validadores atacantes. Em vez de liberar os votos para manter uma divisão entre dois forks, eles usam seus votos em momentos oportunos para justificar pontos de verificação que alternam entre o fork A e o fork B. Esse vai e vem de justificações entre dois forks impede que existam pares de fontes justificadas e pontos de verificação que possam ser finalizados em qualquer cadeia, parando a finalidade.

<YouTube id="xcPxwhrg3Ao"/>

Tanto os ataques de salto, quanto os ataques de balanceamento, dependem de o atacante ter um controle muito preciso sobre o momento das mensagens por toda a rede, o que é improvável. No entanto, as defesas são construídas no protocolo sob a forma de ponderação adicional dada às mensagens rápidas quando comparadas com as lentas. Isso é conhecido como [aceleração de peso do proponente](https://github.com/ethereum/consensus-specs/pull/2730). Para se defender contra ataques de salto, o algoritmo escolhido para o fork foi atualizado de modo que o último ponto de verificação justificado somente possa mudar para uma cadeia alternativa durante o [primeiro 1/3 dos slots em cada época](https://ethresear.ch/t/prevention-of-bouncing-attack-on-ffg/6114). Essa condição impede que o invasor economize votos para implantar mais tarde — o algoritmo de escolha do fork simplesmente permanece fiel ao ponto de verificação escolhido no primeiro 1/3 da época, durante o qual os validadores mais honestos teriam votado.

Combinadas, essas medidas criam um cenário em que um proponente de blocos honesto emite seu bloco muito rapidamente após o início do slot, então há um período de ~1/3 de um slot (4 segundos), no qual esse novo bloco pode fazer com que o algoritmo de escolha de fork alterne para outra cadeia. Depois desse mesmo prazo, as atestações que chegam de validadores lentos têm peso reduzido em comparação com os que chegaram mais cedo. Isso favorece fortemente os proponentes e validadores rápidos na determinação da cabeça da cadeia e reduz substancialmente a probabilidade de um ataque de salto ou balanceamento bem-sucedido.

É importante observar que o proponente apenas defende contra “reorganizações baratas”, ou seja, tentativas feitas por um invasor com um stake pequeno. Na verdade, o próprio acelerador proponente pode ser induzido por partes interessadas maiores. Os autores [desta postagem](https://ethresear.ch/t/change-fork-choice-rule-to-mitigate-balancing-and-reorging-attacks/11127) descrevem como um invasor com 7% de stake pode implantar seus votos estrategicamente para enganar validadores honestos para construir sobre seu fork, reorganizando um bloco honesto. Esse ataque foi concebido assumindo condições de latência ideais muito improváveis. As probabilidades são ainda muito grandes para o invasor, e o stake maior também significa mais capital em risco e um desincentivo econômico maior.

Um [ataque de balanceamento especificamente direcionado à regra de LMD](https://ethresear.ch/t/balancing-attack-lmd-edition/11853) também foi proposto, o que foi sugerido para ser viável, apesar do aumento do proponente. Um invasor cria duas cadeias concorrentes equivocando sua proposta de bloco e propagando cada bloco para cerca de metade da rede cada, estabelecendo um equilíbrio aproximado entre os forks. Em seguida, os validadores em conluio confundem seus votos, calculando o tempo para que metade da rede receba seus votos no fork `A` primeiro, e a outra metade receba seus votos no fork `B` primeiro. Já que a regra de LMD descarta o segundo certificado e mantém apenas o primeiro para cada validador, metade da rede vê os votos para `A` e nenhum para `B`, sendo que a outra metade vê votos para `B` e nenhum para `A`. Os autores descrevem a regra de LMD como dando ao adversário “poder notável” para montar um ataque de balanceamento.

Esse vetor de ataque LMD foi fechado [atualizando o algoritmo de escolha de fork](https://github.com/ethereum/consensus-specs/pull/2845) de modo que ele descarte os validadores equivocados da consideração da escolha do fork. Os validadores equivocados também têm sua futura influência descontada pelo algoritmo de escolha do fork. Isso evita o ataque de balanceamento descrito acima e mantém também resiliência contra ataques em avalanche.

Outra categoria de ataque, chamada [**ataques em avalanche**](https://ethresear.ch/t/avalanche-attack-on-proof-of-stake-ghost/11854/3), foi descrita em um [artigo de março de 2022](https://arxiv.org/pdf/2203.01315.pdf). Para montar um ataque em avalanche, o invasor precisa controlar vários proponentes de bloco consecutivos. Em cada um dos slots da proposta de bloco, o invasor retém seus blocos, coletando-os até que a cadeia honesta atinja um peso igual de sub-árvore com os blocos retidos. Depois, os blocos retidos são liberados para causarem o máximo de equívoco. Os autores sugerem que o proponente impulsionando — a defesa primária contra os ataques de balanceamento e salto — não protege contra algumas variantes de ataque em avalanche. No entanto, os autores também só demonstraram o ataque a uma versão altamente idealizada do algoritmo de escolha de fork do Ethereum (eles usaram GHOST sem LMD).

O ataque em avalanche é mitigado pela porção de LMD do algoritmo de escolha do fork LMD-GHOST. LMD significa “latest-message-driven” (dirigido à última mensagem) e se refere a uma tabela mantida por cada validador contendo a última mensagem recebida de outros validadores. Esse campo só é atualizado se a nova mensagem for de um slot posterior ao que já está na tabela para um validador em particular. Na prática, isso significa que em cada slot, a primeira mensagem recebida é aquela que aceitou e todas as mensagens adicionais são equívocos a serem ignorados. Por outras palavras, os clientes de consenso não contam equívocos — eles usam a primeira mensagem de cada validador e os equívocos são simplesmente descartados, evitando ataques em avalanche.

Há várias outras atualizações futuras possíveis para a regra de escolha do fork que podem aumentar a segurança fornecida pelo impulsionador do proponente. Uma delas é a [visualização mesclada](https://ethresear.ch/t/view-merge-as-a-replacement-for-proposer-boost/13739), na qual os atestadores congelam sua visualização da escolha do fork `n` segundos antes do início de um slot e, em seguida, o proponente ajuda a sincronizar a visualização da cadeia pela rede. Outra potencial melhoria é a [finalidade de slot único](https://notes.ethereum.org/@vbuterin/single_slot_finality), que protege contra ataques baseados no tempo da mensagem, finalizando a cadeia após apenas um slot.

#### Atraso de finalidade {#finality-delay}

[O mesmo artigo](https://econcs.pku.edu.cn/wine2020/wine2020/Workshop/GTiB20_paper_8.pdf) que descreveu primeiro o ataque de reorganização de bloco único de baixo custo também descreveu um ataque de atraso de finalidade (também conhecido como “falha de vivacidade”) que depende de o atacante ser o proponente do bloco para um bloco de limite de época. Isso é crítico porque esses blocos de limite de época se tornam os pontos de verificação que o Casper FFG usa para finalizar partes da cadeia. O invasor simplesmente mantém seu bloco até que um número suficiente de validadores honestos usem seus votos FFG em favor do bloco anterior com limite de época como o atual alvo de finalização. Em seguida, eles liberam seus blocos retidos. Eles atestam seus blocos e os restantes validadores honestos o fazem também criando forks com pontos de verificação de destino diferentes. Se o fizerem no momento certo, evitarão a finalidade, pois não haverá uma supermaioria de 2/3 atestando outro fork. Quanto menor for o stake, mais preciso deverá ser o tempo, pois o invasor controla menos atestações diretamente, e menor será a probabilidade de o invasor controlar o validador propondo um determinado bloco de limites de época.

#### Ataques de longo alcance {#long-range-attacks}

Também existe uma classe de ataque específico para blockchains de prova de participação que envolve um validador que participou do bloco de origem, mantendo um fork separado da blockchain junto com o honesto, finalmente convencendo o validador honesto definido a mudar para ele em algum tempo oportuno mais tarde. Este tipo de ataque não é possível no Ethereum devido ao dispositivo de finalidade que garante que todos os validadores concordem com o estado da cadeia honesta em intervalos regulares (“pontos de verificação”). Esse mecanismo simples neutraliza invasores de longo alcance, pois os clientes do Ethereum simplesmente não irão reorganizar blocos finalizados. Novos nós que participam da rede fazem isso encontrando um hash confiável do estado recente (um “ponto de verificação de[subjetividade fraca](https://blog.ethereum.org/2014/11/25/proof-stake-learned-love-weak-subjectivity/)”) e usando-o como um pseudo bloco de origem sobre o qual se construir. Isso cria um “gateway de confiança” para um novo nó que entra na rede antes de começar a verificar as informações por si mesmo.

#### Negação de serviço {#denial-of-service}

O mecanismo PoS da Ethereum escolhe um único validador do conjunto total de validadores para ser o proponente de blocos em cada slot. Isso pode ser calculado usando uma função conhecida publicamente e é possível para um adversário identificar o próximo proponente de blocos um pouco antes de sua proposta de bloco. Em seguida, o invasor pode enviar spam ao proponente de bloco para evitar que eles troquem informações com seus pares. Para o resto da rede, vai parecer que o proponente de blocos estava offline e que o slot simplesmente iria ficar vazio. Isso pode ser uma forma de censura contra validadores específicos, impedindo-os de adicionar informações à blockchain. A implementação de eleições de líder único secretas (SSLE) ou eleições de líder não único secretas atenuarão os riscos de DoS, pois só o proponente de blocos sabe que foram eles selecionados e a seleção não é conhecida antecipadamente. Isso ainda não está implementado, mas é uma área ativa de [pesquisa e desenvolvimento](https://ethresear.ch/t/secret-non-single-leader-election/11789).

Tudo isso aponta para o fato de que é muito difícil atacar com sucesso o Ethereum com um pequeno stake. Os ataques viáveis descritos aqui requerem um algoritmo de seleção de fork idealizado, condições de rede improváveis, ou os vetores de ataque já foram fechados com patches relativamente menores para o software cliente. Isso, claro, não exclui a possibilidade de existirem zero dias na natureza, mas demonstra a alta exigência de aptidão técnica, conhecimento da camada de consenso e sorte necessárioa para que um invasor minoritário de stakes seja eficaz. Do ponto de vista de um invasor, sua melhor aposta podeá ser a de acumular o máximo de ethers possível e retornar equipado com uma maior proporção de stakes total.

### Ataques usando >= 33% do stake total {#attackers-with-33-stake}

Todos os ataques mencionados anteriormente neste artigo se tornam mais propensos a terem êxito quando o invasor tiver mais ethers em stake para votar, e mais validadores que podem ser escolhidos para propor blocos em cada slot. Um validador malicioso pode buscar, portanto, controlar o máximo possível de ethers em stake.

33% do ether em stake é um ponto de referência para um invasor porque, com qualquer coisa maior que essa quantidade, eles têm a habilidade de evitar que a cadeia finalize sem ter que controlar com precisão as ações dos outros validadores. Eles simplesmente podem desaparecer todos juntos. Se 1/3 ou mais do ether em stake estiver atestando de forma maliciosa ou falhando em atestar, não poderá existir uma supermaioria de 2/3 e a cadeia não poderá finalizar. A defesa contra isso é o vazamento de inatividade. O vazamento de inatividade identifica os validadores que estão falhando em atestar ou atestando contrário à maioria. O ether em stake pertencente a esses validadores que não atestam é esvaziado gradualmente até que, por fim, eles representem coletivamente menos de 1/3 do total, de modo que a cadeia possa ser finalizada novamente.

O propósito do vazamento de inatividade é finalizar a cadeia novamente. No entanto, o invasor também perde uma parte do seu ether em stake. Inatividade persistente entre validadores que representam 33% do ether total em stake é muito caro, mesmo que os validadores não tenham sido removidos.

Presumindo que a rede Ethereum seja assíncrona (ou seja, há atrasos entre as mensagens sendo enviadas e recebidas), um atacante controlando 34% do stake total poderia causar dupla finalidade. Isso ocorre porque o invasor pode se enganar quando é escolhido para ser produtor de bloco e votar duas vezes com todos os seus validadores. Isso cria uma situação em que existe um fork da blockchain, cada um com 34% do ether em stake votando por ele. Cada fork requer apenas 50% dos validadores restantes para votar em seu favor para que ambos os forks sejam apoiados por uma supermaioria, devendo nesses caso ambas as cadeias poderem finalizar (pois 34% dos invasores validadores + metade do restante de 66% = 67% em cada fork). Cada um dos blocos concorrentes teria que ser recebido por cerca de 50% dos validadores honestos para que esse ataque seja viável somente quando o invasor tiver algum grau de controle sobre o tempo das mensagens que se propagam pela rede, para que eles possam levar metade dos validadores honestos para cada cadeia. O invasor destruiria necessariamente toda o seu stake (34% de ~10 milhões de ethers com o conjunto de validadores atual) para alcançar essa dupla finalidade, pois 34% de seus validadores teriam voto duplo simultaneamente — uma infração sujeita a remoção com penalidade máxima. A defesa contra este ataque é o custo muito elevado de destruir 34% do total do ethers em stake. Para se recuperar desse ataque, seria necessário que a comunidade Ethereum se coordenasse “fora de banda” e concordasse em seguir um ou outro dos forks e ignorar o outro.

### Invasores usando ~50% do stake total {#attackers-with-50-stake}

A 50% do ether em stake, um grupo malicioso de validadores poderia, teoricamente, dividir a cadeia em dois forks de tamanho igual e, em seguida, simplesmente usar todo seu stake de 50% para votar contrariamente ao conjunto de validadores honestos, mantendo assim os dois forks e impedindo a finalidade. O vazamento de inatividade em ambos os forks levaria, por fim, ambas as cadeias a finalizar. A essa altura, a única opção é recorrer a uma recuperação social.

É muito improvável que um grupo adversário de validadores possa controlar, de forma consistente, precisamente 50% do stake total, dado um determinado grau de fluxo em números de validadores honestos, latência de rede, etc. Porém, o enorme custo de montar tal ataque, combinado com a baixa probabilidade de sucesso, parece ser um grande desincentivo para um invasor racional, especialmente quando um pequeno investimento adicional para obter _mais do que_ 50% proporciona muito mais poder.

Com >50% do stake total, o invasor poderia dominar o algoritmo de escolha do fork. Nesse caso, o invasor poderia atestar com o voto majoritário, dando-lhes controle suficiente para fazer pequenas reorganizações sem precisar enganar clientes honestos. Os validadores honestos seguiriam o exemplo, pois seu algoritmo de escolha de fork também veria a cadeia preferida do invasor como a mais pesada, permitindo que a cadeia finalize. Isso permite ao invasor censurar certas transações, fazer reorganizações de curto alcance e extrair o máximo de MEV reordenando blocos a seu favor. A defesa contra isso é o enorme custo de um stake majoritário (atualmente, pouco menos de 19 bilhões de dólares) posto em risco por um invasor, pois a camada social é susceptível de intervir e adotar um fork de minoria honesta, desvalorizando o stake do invasor drasticamente.

### Invasores usando >= 66% do stake total {#attackers-with-66-stake}

Um invasor com 66% ou mais do ether total em stake pode finalizar sua cadeia preferida sem ter que coagir nenhum validador honesto. O invasor pode simplesmente votar no seu fork preferido e depois finalizá-lo, simplesmente porque ele pode votar com uma supermaioria desonesta. Como parte interessada de supermaioria, o invasor sempre controlaria o conteúdo dos blocos finalizados, com o poder de gastar, retroceder e gastar novamente, censurar determinadas transações e reorganizar a cadeia como quisesse. Comprando mais ethers para controlar 66% em vez de 51%, o invasor está efetivamente comprando a habilidade de fazer reorganizações ex post e reversões de finalidade (ou seja, alterar o passado e controlar o futuro). As únicas defesas reais aqui são o enorme custo de 66% do total do ethers em stake e a opção de voltar à camada social para coordenar a adoção de um fork alternativo. Podemos explorar isso com mais detalhes na próxima seção.

## Pessoas: a última linha de defesa {#people-the-last-line-of-defense}

Se os validadores desonestos conseguirem finalizar sua versão preferida da cadeia, a comunidade Ethereum é colocada em uma situação difícil. A cadeia padrão inclui uma seção desonesta produzida em seu histórico, enquanto validadores honestos podem acabar sendo punidos por atestar uma cadeia alternativa (honesta). Observe que uma cadeia finalizada, mas incorreta, também poderia surgir de um bug em um cliente maioritário. No final, o último recurso é confiar na camada social — Camada 0 — para resolver a situação.

Um dos pontos fortes do consenso do Ethereum no PoS é que há uma [gama de estratégias defensivas](https://youtu.be/1m12zgJ42dI?t=1712) que a comunidade pode empregar diante de um ataque. Uma resposta mínima poderia ser tirar forçadamente os validadores dos atacantes da rede sem nenhuma penalidade adicional. Para entrar novamente na rede, o invasor teria que entrar em uma fila de ativação que garantisse que o validador definido crescesse gradualmente. Por exemplo, adicionar validadores suficientes para dobrar a quantidade de ethers em stake leva cerca de 200 dias, efetivamente fazendo com que os validadores honestos ganhem 200 dias antes que o atacante possa tentar outro ataque de 51%. No entanto, a comunidade também poderia decidir penalizar o invasor de forma mais severa, revogando recompensas passadas ou queimando alguma porção (até 100%) do seu capital em stake.

Seja qual for a penalidade imposta ao invasor, a comunidade também tem de decidir em conjunto se a cadeia desonesta, apesar de ser a favorita pelo algoritmo de escolha do fork codificado nos clientes Ethereum, é de fato inválida e se a comunidade deve construir por cima da cadeia honesta. Os validadores honestos poderiam concordar coletivamente em construir sobre um fork aceito pela comunidade da blockchain Ethereum que poderia, por exemplo, ter feito o fork da cadeia padrão antes de o ataque começar ou ter os validadores dos invasores removidos forçadamente. Os validadores honestos seriam incentivados a construir nessa cadeia, pois eles evitariam as penalidades aplicadas a eles por falhar (devidamente) em atestar a cadeia do invasor. Agências de câmbio, rampas de acesso e aplicativos construídos no Ethereum provavelmente prefeririam estar na cadeia honesta e seguir os validadores honestos na blockchain honesta.

No entanto, isso constituiria um desafio substancial em termos de governança. Alguns usuários e validadores certamente se perderiam ao retornar à cadeia honesta. As transações em blocos validados após o ataque poderiam ser revertidas, perturbando a camada de aplicação, o que simplesmente compromete a ética de alguns usuários que tendem a acreditar que “código é lei”. Agências de câmbio e aplicações teriam provavelmente vinculado ações fora da cadeia a transações na cadeia, que agora podem ser revertidas, começando uma cascata de retratações e revisões que seria difícil de desfazer de forma justa, especialmente se os ganhos obtidos ilicitamente tiverem sido misturados, depositados em DeFi ou em outros derivados com efeitos secundários para usuários honestos. Sem dúvida que alguns usuários, talvez mesmo institucionais, já teriam se beneficiado da cadeia desonesta, seja por esperteza ou por acaso, e poderiam se opor a um fork para proteger seus ganhos. Já foram feitos pedidos para simular a resposta da comunidade a ataques de >51%, a fim de coordenar uma ação de mitigação sensata que possa ser executada rapidamente. Existem algumas discussões úteis de Vitalik no ethresear.ch [aqui](https://ethresear.ch/t/timeliness-detectors-and-51-attack-recovery-in-blockchains/6925) e [aqui](https://ethresear.ch/t/responding-to-51-attacks-in-casper-ffg/6363) e no Twitter [aqui](https://twitter.com/skylar_eth/status/1551798684727508992?s=20&t=oHZ1xv8QZdOgAXhxZKtHEw). O objetivo de uma resposta social coordenada é o de ser muito direcionada e específica para punir o invasor e minimizar os efeitos para outros usuários.

Governança já é um tema complicado. Gerenciar uma resposta de emergência de Camada 0 para uma cadeia de finalização desonesta seria, sem dúvida, desafiante para a comunidade Ethereum, mas [aconteceu](https://ethereum.org/en/history/#dao-fork-summary) - [duas vezes](https://ethereum.org/en/history/#tangerine-whistle) no histórico do Ethereum).

No entanto, há algo que é bastante satisfatório na última tentativa no mundo real. Em última análise, mesmo com essa pilha fenomenal de tecnologia acima de nós, se o pior alguma vez acontecer, pessoas reais terão de coordenar a solução.

## Resumo {#summary}

Esta página explorou algumas das maneiras como os invasores poderiam tentar explorar o protocolo de consenso da prova de participação do Ethereum. Reorganizações e atrasos de finalidade foram explorados por invasores com proporções cada vez maiores do total de ethers em stake. No geral, um invasor mais rico tem mais chances de sucesso porque seu stake se traduz em poder de voto, que ele pode usar para influenciar o conteúdo de futuros blocos. Em certas quantidades limite de ether em stake, o poder do invasor aumenta de nível:

33%: atraso de finalidade

34%: atraso de finalidade, dupla finalidade

51%: atraso de finalidade, dupla finalidade, censura, controle sobre o futuro da blockchain

66%: atraso de finalidade, dupla finalidade, censura, controle sobre o futuro e passado da blockchain

Há também uma série de ataques mais sofisticados que exigem pequenas quantidades de ether em stake, mas dependem de um invasor muito sofisticado que tenha bom controle sobre o tempo das mensagens para influenciar o conjunto de validadores honestos a seu favor.

Em geral, apesar desses potenciais vetores de ataque, o risco de um ataque bem-sucedido é baixo, certamente menor que os equivalentes da prova de trabalho. Isso é devido ao enorme custo do ether colocado em risco por um invasor visando esmagar validadores honestos com seu poder de voto. A camada de incentivo de “cenoura e bastão” incorporada protege contra a maioria das condutas ilegais, especialmente para os invasores de baixo stake. Ataques mais sutis de salto e balanceamento também têm poucas chances de êxito, pois as condições reais da rede tornam o controle detalhado da entrega de mensagens a subconjuntos específicos de validadores muito difícil de atingir, e as equipes de clientes fecharam rapidamente os vetores de ataque de salto, balanceamento e avalanche conhecidos usando patches simples.

Para solucionar ataques de 34%, 51% ou 66% seria provavelmente necessário uma coordenação social fora de banda. Embora isso provavelmente seja doloroso para a comunidade, a capacidade de uma comunidade responder fora da banda é um forte desincentivo para um invasor. A camada social do Ethereum é o ponto final — um ataque tecnicamente bem-sucedido ainda poderia ser neutralizado se a comunidade concordar em adotar um fork honesto. Haveria uma corrida entre o invasor e a comunidade Ethereum — os bilhões de dólares gastos em um ataque de 66% seriam provavelmente eliminados por um ataque de coordenação social bem-sucedido, se fossem entregues com rapidez suficiente. Isso deixaria o invasor com enormes quantidades de ether em stake sem liquidez em uma cadeia desonesta conhecida, ignorada pela comunidade Ethereum. A probabilidade dessa ação ser lucrativa é tão baixa que se torna um dissuasor eficaz. É por isso que o investimento na manutenção de uma camada social coesa com valores fortemente alinhados é tão importante.

## Leitura adicional {#further-reading}

- [Versão mais detalhada desta página](https://mirror.xyz/jmcook.eth/YqHargbVWVNRQqQpVpzrqEQ8IqwNUJDIpwRP7SS5FXs)
- [Vitalik sobre finalidade de liquidação](https://blog.ethereum.org/2016/05/09/on-settlement-finality/)
- [Artigo sobre o GHOST LMD](https://arxiv.org/abs/2003.03052)
- [Artigo sobre o Casper-FFG](https://arxiv.org/abs/1710.09437)
- [Artigo sobre o Gasper](https://arxiv.org/pdf/2003.03052.pdf)
- [Especificações de consenso de aumento de peso do proponente](https://github.com/ethereum/consensus-specs/pull/2730)
- [Ataques de salto em ethresear.ch](https://ethresear.ch/t/prevention-of-bouncing-attack-on-ffg/6114)
- [Pesquisa SSLE](https://ethresear.ch/t/secret-non-single-leader-election/11789)