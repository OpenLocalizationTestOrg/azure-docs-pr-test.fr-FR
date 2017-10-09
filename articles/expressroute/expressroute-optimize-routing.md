---
title: "Optimiser le routage ExpressRoute : Azure | Microsoft Docs"
description: "Cette page fournit plus d’informations sur comment toooptimize routage lorsque vous avez plusieurs ExpressRoute des circuits qui se connecter entre Microsoft et votre réseau d’entreprise."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
ms.assetid: fca53249-d9c3-4cff-8916-f8749386a4dd
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/06/2017
ms.author: charwen
ms.openlocfilehash: ebcfb638f67a9ac78c3e476668bfd0bb0ffb9985
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-expressroute-routing"></a>Optimiser le routage ExpressRoute
Lorsque vous avez plusieurs circuits ExpressRoute, vous avez plusieurs tooMicrosoft tooconnect de chemin d’accès. Par conséquent, routage non optimaux peut se produire - autrement dit, le trafic peut prendre un tooreach de chemin d’accès plu Microsoft et Microsoft tooyour réseau. Hello plu hello chemin d’accès réseau, une latence plus élevée hello hello. La latence a un impact direct sur les performances d’application ainsi que sur l’expérience utilisateur. Cet article illustrent ce problème et expliquent comment le routage à l’aide de toooptimize hello technologies standard de routage.

## <a name="suboptimal-routing-from-customer-toomicrosoft"></a>Non optimal de routage à partir du client tooMicrosoft
Jetons un œil fermer au problème de routage hello par un exemple. Imaginez que vous disposez de deux bureaux dans hello des États-Unis, à Los Angeles et de New York. Vos bureaux sont connectés sur un réseau étendu (WAN), qui peut être votre propre réseau principal ou le VPN IP de votre fournisseur de services. Vous avez deux circuits ExpressRoute, un dans US West et l’autre dans US East, qui sont également connectés sur hello WAN. Évidemment, vous avez deux chemins d’accès tooconnect toohello (Microsoft network). Imaginez à présent que vous déployiez un service Azure (par exemple, Azure App Service) dans l’Ouest et dans l’Est des États-Unis. Votre intention est tooconnect vos utilisateurs à Los Angeles tooAzure région ouest des États-Unis et vos utilisateurs à New York tooAzure États-Unis, car votre administrateur de service publie que les utilisateurs dans chaque office access hello à proximité de services Windows Azure pour une expérience optimale. Malheureusement, le plan de hello fonctionne bien pour les utilisateurs de hello côte est, mais pas pour les utilisateurs de côte ouest hello. Hello hello problème est dû de suivant de hello. Sur chaque circuit ExpressRoute, nous publier tooyou préfixe hello dans Azure US East (23.100.0.0/16) à la fois et le préfixe de hello dans Azure US West (13.100.0.0/16). Si vous ne connaissez pas le préfixe est à partir de la région, vous n’êtes pas en mesure de tootreat il différemment. Le réseau WAN peut considérer les deux des préfixes de hello plus proche est tooUS à la région ouest des États-Unis, par conséquent, router les deux toohello d’utilisateurs office circuit ExpressRoute dans US East. Final de hello, vous aurez nombreux utilisateurs mécontenter Bonjour Los Angeles office.

![Problème de ExpressRoute cas 1 - non optimal de routage à partir du client tooMicrosoft](./media/expressroute-optimize-routing/expressroute-case1-problem.png)

### <a name="solution-use-bgp-communities"></a>Solution : utilisez des communautés BGP
toooptimize routage pour les utilisateurs d’office, vous devez tooknow préfixe provient Azure région ouest des États-Unis et qui Azure États-Unis. Nous encodons ces informations à l’aide des [valeurs de communauté BGP](expressroute-routing.md). Nous avons attribué un tooeach de valeur unique BGP Communauté région Azure, par exemple « 12076:51004 » pour l’Est des États-Unis et « 12076:51006 » pour l’Ouest des États-Unis. À présent que vous savez à quelles régions Azure correspondent les préfixes, vous pouvez configurer les préférences de circuit ExpressRoute. Étant donné que nous utilisons les informations de routage du tooexchange hello BGP, vous pouvez utiliser BGP préférence Local tooinfluence routage. Dans notre exemple, vous pouvez affecter un supérieur préférence local valeur too13.100.0.0/16 dans US West que dans la région est des États-Unis, de la même manière, un supérieur préférence local valeur too23.100.0.0/16 dans US East que dans la région ouest des États-Unis. Cette configuration permet de garantir que, lorsque les deux tooMicrosoft de chemins d’accès sont disponibles, vos utilisateurs à Los Angeles prennent circuit ExpressRoute de hello dans la région ouest des États-Unis tooconnect tooAzure région ouest des États-Unis que vos utilisateurs à New York prennent hello ExpressRoute dans tooAzure de région est des États-Unis . Le routage est optimisé des deux côtés. 

![Solution ExpressRoute n° 1 : utilisez des communautés BGP](./media/expressroute-optimize-routing/expressroute-case1-solution.png)

> [!NOTE]
> Hello même technique, à l’aide de préférence Local, peut être appliqué toorouting à partir du client tooAzure réseau virtuel. Nous ne baliser des préfixes de toohello valeur BGP Communauté publiés à partir du réseau de tooyour Azure. Toutefois, étant donné que vous savez qui du déploiement de votre réseau virtuel est toowhich fermeture de votre bureau, vous pouvez configurer vos routeurs en conséquence une tooanother de circuit ExpressRoute tooprefer.
>
>

## <a name="suboptimal-routing-from-microsoft-toocustomer"></a>Non optimal de routage à partir de Microsoft toocustomer
Voici un autre exemple dans lequel les connexions à partir de Microsoft prennent un tooreach de chemin d’accès plu votre réseau. Dans ce cas, vous utilisez des serveurs Exchange locaux et Exchange Online dans un [environnement hybride](https://technet.microsoft.com/library/jj200581%28v=exchg.150%29.aspx). Vos sites sont connecté tooa WAN. Vous publiez des préfixes hello de vos serveurs locaux dans les deux de vos tooMicrosoft bureaux par le biais des circuits ExpressRoute hello deux. Initie connexions toohello sur des serveurs locaux dans le cas par exemple, la migration des boîtes aux lettres Exchange Online. Malheureusement, hello connexion tooyour Los Angeles office est routé toohello circuit ExpressRoute dans US East avant d’entamer la côte ouest de toohello entière de retour continent hello. cause du problème de hello Hello est similaire toohello tout d’abord un. Sans indicateur de n’importe quel réseau de Microsoft hello ne peut pas déterminer le préfixe de client est tooUS fermer et les fermer tooUS ouest. Il produit office de tooyour toopick hello chemin d’accès incorrect à Los Angeles.

![ExpressRoute cas N° 2 - non optimal de routage à partir de Microsoft toocustomer](./media/expressroute-optimize-routing/expressroute-case2-problem.png)

### <a name="solution-use-as-path-prepending"></a>Solution : ajoutez le préfixe AS PATH
Il existe deux problème toohello de solutions. Hello tout d’abord une est que vous publiez simplement votre préfixe local à votre Bureau à Los Angeles, 177.2.0.0/31, sur le circuit ExpressRoute de hello dans US West et votre site de préfixe pour votre bureau de New York, 177.2.0.2/31, sur le circuit ExpressRoute de hello dans US East. Par conséquent, il n'existe qu’un seul chemin pour tooeach tooconnect de Microsoft de vos bureaux. Il n’existe aucune ambiguïté et le routage est optimisé. Grâce à cette conception, vous devez toothink sur votre stratégie de basculement. Bonjour événement hello tooMicrosoft de chemin d’accès via ExpressRoute est interrompue, vous devez toomake sûr qu’Exchange Online peuvent toujours se connecter tooyour sur des serveurs locaux. 

solution de deuxième Hello est que vous continuer tooadvertise des préfixes de hello sur les deux circuits ExpressRoute ; en outre vous devez nous fournir une indication de préfixe est toowhich fermer un de vos bureaux. Étant donné que nous prenons en charge le chemin d’accès de protocole BGP en ajoutant au début, vous pouvez configurer hello en tant que chemin pour votre préfixe tooinfluence le routage. Dans cet exemple, vous pouvez augmenter hello en tant que chemin de 172.2.0.0/31 dans US East afin que nous préfèreront circuit ExpressRoute de hello dans la région ouest des États-Unis pour le trafic destiné à ce préfixe (comme notre réseau pense que préfixe de toothis hello chemin d’accès est plus court dans l’ouest de hello). De même, vous pouvez augmenter hello en tant que chemin de 172.2.0.2/31 dans US West afin que nous allons préférez circuit ExpressRoute de hello dans US East. Le routage est optimisé pour les deux bureaux. Grâce à cette conception, si un circuit ExpressRoute est défaillant, Exchange Online peut toujours vous joindre via un autre circuit ExpressRoute ainsi que par le biais de votre réseau étendu. 

> [!IMPORTANT]
> Nous remove privé numéros Bonjour chemin d’accès en tant que pour les préfixes hello reçu sur Microsoft Peering. Vous devez tooappend publique sous forme de nombres dans tooinfluence hello en tant que chemin d’accès au routage pour Microsoft Peering.
> 
> 

![Solution ExpressRoute n° 2 : ajoutez le préfixe AS PATH](./media/expressroute-optimize-routing/expressroute-case2-solution.png)

> [!NOTE]
> Alors que les exemples hello sont destiné à Microsoft et homologations Public, nous prennent en charge hello les mêmes fonctionnalités pour l’homologation privée hello. En outre, ajoutant au début du chemin d’accès comme hello fonctionne dans un même circuit ExpressRoute, sélection de hello tooinfluence des chemins d’accès primaire et secondaire hello.
> 
> 

## <a name="suboptimal-routing-between-virtual-networks"></a>Routage non optimal entre des réseaux virtuels
Grâce à ExpressRoute, vous pouvez activer le réseau virtuel tooVirtual réseau (qui est également appelé « Réseau virtuel ») communication en les liant circuit ExpressRoute de tooan. Lorsque vous les liez des circuits ExpressRoute toomultiple, routage non optimaux peut se produire entre hello des réseaux virtuels. Prenons un exemple. Vous disposez de deux circuits ExpressRoute, l’un dans l’Ouest des États-Unis et l’autre dans l’Est des États-Unis. Dans chaque région, vous avez deux réseaux virtuels. Vos serveurs web sont déployés dans un réseau virtuel et les serveurs d’applications de hello autres. Pour assurer la redondance, lien vous hello deux réseaux virtuels dans chaque circuit ExpressRoute région tooboth hello local et distant circuit ExpressRoute de hello. Comme indiqué ci-dessous, à partir de chaque réseau virtuel il existe deux chemins d’accès toohello autre réseau virtuel. Hello réseaux virtuels ne connaissez pas le circuit ExpressRoute est local et celui qui est distant. Par conséquent, comme ils le font égal-coût-Multi-Path (ECMP) routage tooload équilibrer inter-réseau virtuel trafic, certains flux de trafic hello chemin le plus long et acheminés au circuit ExpressRoute à distance de hello.

![Scénario ExpressRoute n° 3 : routage non optimal entre réseaux virtuels](./media/expressroute-optimize-routing/expressroute-case3-problem.png)

### <a name="solution-assign-a-high-weight-toolocal-connection"></a>Solution : affectez à une connexion de toolocal poids élevé
solution de Hello est simple. Étant donné que vous savez où circuits de réseaux virtuels et hello hello, vous pouvez nous indiquer le chemin d’accès, préférez chaque réseau virtuel. Spécifiquement pour cet exemple, vous affectez supérieur poids toohello connexion locale à la connexion à distance de toohello (consultez l’exemple de configuration hello [ici](expressroute-howto-linkvnet-arm.md#modify-a-virtual-network-connection)). Lorsqu’un réseau virtuel reçoit le préfixe hello hello autre réseau virtuel sur plusieurs connexions il préfère connexion de hello avec hello plus élevé poids toosend le trafic destiné à ce préfixe.

![Solution de ExpressRoute cas 3 - affecter des poids élevé toolocal connexion](./media/expressroute-optimize-routing/expressroute-case3-solution.png)

> [!NOTE]
> Vous pouvez également influer sur routage réseau virtuel tooyour sur un réseau local, si vous avez plusieurs circuits ExpressRoute, en configurant les poids hello d’une connexion au lieu d’appliquer le chemin d’accès en ajoutant le préfixe, une technique décrite dans le deuxième scénario hello ci-dessus. Pour chaque préfixe, nous allons toujours examiner poids de connexion hello avant hello longueur de chemin d’accès en tant que lorsque vous décidez comment le trafic de toosend.
>
>
