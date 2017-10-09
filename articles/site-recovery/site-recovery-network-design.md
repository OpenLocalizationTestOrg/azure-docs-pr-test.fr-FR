---
title: "aaaDesigning votre infrastructure réseau pour la récupération d’urgence | Documents Microsoft"
description: "Cet article aborde les considérations de conception de réseau pour Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: jwhit
editor: 
ms.assetid: ce787731-d930-4f00-a309-e2fbc2e1f53b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/20/2017
ms.author: pratshar
ms.openlocfilehash: 18bafa1b8b334192bfaf2f4aeba9f090011041ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="designing-your-network-for-disaster-recovery"></a>Conception de votre réseau pour la récupération d’urgence

Cet article est dirigée tooIT professionnels qui sont responsables de la conception, l’implémentation et la prise en charge de la continuité d’activité et l’infrastructure de récupération d’urgence, et qui souhaitent tooleverage Microsoft Azure Site Recovery (ASR) toosupport et améliorer leurs services BCDR. Cet article traite des considérations pratiques en matière de structuration réseau au niveau du site de récupération d’urgence, qu’il s’agisse d’Azure ou d’un autre site local. 

## <a name="overview"></a>Vue d'ensemble
[Azure Site Recovery (ASR)](https://azure.microsoft.com/services/site-recovery/) est un service Microsoft Azure qui orchestre la protection de hello et la récupération de vos applications virtualisées à des fins commerciales la continuité des activités d’urgence (BCDR) de récupération. Ce document est prévue tooguide hello lecteur tout au long des processus de hello de la conception des réseaux de hello, en mettant l’accent sur la conception des plages d’adresses IP et des sous-réseaux sur site de récupération d’urgence hello, lors de la réplication des machines virtuelles (VM) à l’aide de la récupération de Site.

En outre, cet article explique comment Site Recovery permet d’architecture et l’implémentation d’un centre de données virtuel multisite toosupport des services BCDR au moment de test ou d’urgence.

Dans un monde où tout le monde attend 24/7 connectivité, il est plus important que jamais tookeep votre infrastructure et vos applications en hausse et en cours d’exécution. Hello de continuité des activités et récupération d’urgence (BCDR) vise toorestore échoué de composants afin de l’organisation de hello peut reprendre rapidement les opérations normales. Développement toodeal stratégies de récupération d’urgence avec les événements peu probable, catastrophiques est très difficile. Il s’agit en raison de la difficulté inhérente de toohello permettant de prévoir les futures hello, notamment en matière de tooimprobable événements et hello haute coût tooprovide des mesures appropriées de protection contre les catastrophes portée considérable.

Essentiels pour la planification de BCDR, un objectif de délai de récupération (RTO) et un objectif de point de récupération (RPO) doivent être définis dans le cadre d’un plan de récupération d’urgence. Lorsqu’un incident ne survienne centre de données hello client, à l’aide d’Azure Site Recovery, les clients peuvent rapidement (RTO faible) à mettre en ligne leurs machines virtuelles répliquées situées dans le centre de données secondaire hello ou Microsoft Azure avec une perte minimale de données (RPO faible).

Basculement est rendu possible par la récupération automatique du système qui a initialement copie désignés machines virtuelles de centre de données secondaire hello données primaires center toohello ou tooAzure (selon le scénario de hello) et actualise régulièrement les réplicas de hello. Lors de la planification de l’infrastructure, la conception réseau doit être considérée comme un goulot d’étranglement potentiel, qui peut vous empêcher de remplir les objectifs RTO et RPO de la société.  

Lorsque les administrateurs planifiez toodeploy une solution de récupération d’urgence, une des questions clés hello esprits est comment hello ordinateur virtuel est accessible après que le basculement hello est effectué. Récupération automatique du système permet de hello administrateur toochoose hello réseau toowhich un ordinateur virtuel est connecté tooafter basculement. Si le site principal de hello est Azure, ou il s’agit d’un site local géré par un serveur VMM puis cela à l’aide de mappage réseau. En savoir plus sur [mappage réseau dans Azure tooAzure de récupération d’urgence](site-recovery-network-mapping-azure-to-azure.md) et [mappage réseau à partir de VMM](site-recovery-network-mapping.md)


Lors de la conception réseau hello pour le site de récupération hello, administrateur de hello a deux possibilités :

* Utiliser une autre plage d’adresses IP pour le réseau hello sur site de récupération. Dans ce scénario, obtenez une nouvelle adresse IP virtuels hello après le basculement et hello administrateur a toodo une mise à jour DNS. 
* Utiliser la même plage d’adresses IP pour le réseau hello sur site de récupération hello. Dans certains scénarios, les administrateurs de préférer les adresses IP tooretain hello qu’ils sont sur le site principal de hello même après le basculement de hello. Un administrateur a tooupdate hello itinéraires tooindicate hello nouvel emplacement d’adresses IP de hello dans un scénario normal. Mais dans un scénario hello dans lequel il est déployé un sous-réseau étendu entre hello principal et les sites de récupération hello, en conservant les adresses IP de hello pour les ordinateurs virtuels de hello devient une option intéressante. Étirer un sous-réseau à partir d’un tooan de réseau local réseau Azure ou entre deux réseaux Azure n’est pas possible.  

Lorsque les administrateurs planifiez toodeploy une solution de récupération d’urgence, une des questions clés de hello leur esprit est comment les applications hello seront accessibles une fois le basculement hello est effectué. Les applications modernes sont presque toujours dépendantes du degré de toosome, la mise en réseau physiquement de déplacement d’un service à partir d’un seul site tooanother représente un défi de mise en réseau. Deux méthodes principales permettent de traiter ce problème dans les solutions de récupération d’urgence. Hello première approche consiste toomaintain des adresses IP fixé. En dépit de services hello déplacement et hello hébergeant des serveurs en cours dans plusieurs emplacements physiques, applications prennent configuration d’adresse IP hello avec eux toohello un nouvel emplacement. Hello seconde implique complètement la modification adresse hello pendant la transition de hello en hello le site récupéré. Chaque approche présente plusieurs variantes d’implémentation qui sont résumées ci-dessous.

Lors de la conception réseau hello pour le site de récupération hello, administrateur de hello a deux possibilités :

## <a name="option-1-retain-ip-addresses"></a>Option 1 : Conserver les adresses IP
À partir d’une perspective de processus de récupération d’urgence, à l’aide d’adresses IP fixes apparaît toobe hello plus simple méthode tooimplement, mais il comporte un nombre potentiel de défis qui, dans la pratique, le rendre hello approche les moins fréquents. Azure Site Recovery permet hello les adresses IP tooretain hello dans tous les scénarios. Avant que quelqu'un décide tooretain IP, pensée appropriée doit disposer de contraintes toohello qu'il impose aux fonctionnalités de basculement hello. Examinons les facteurs hello qui peuvent vous aider à toomake qu'une décision tooretain adresses IP, ou non. Cela est possible de deux manières, en utilisant un sous-réseau étiré ou en procédant à un basculement de sous-réseau complet.

### <a name="stretched-subnet"></a>Sous-réseau étiré
Ici, les sous-réseaux hello sont rendue disponible simultanément dans le serveur principal et les emplacements de récupération d’urgence. En termes simples, cela signifie vous pouvez déplacer un serveur et son réseau de hello et un deuxième site IP (couche 3) configuration toohello achemine nouvel emplacement hello trafic toohello automatiquement. Il s’agit de toodeal trivial avec à partir d’un point de vue du serveur, mais il a un nombre de tests :

* Dans la perspective de la couche 2 (couche de liaison de données), un équipement de mise en réseau capable de gérer un VLAN étiré est nécessaire, mais cela n’est plus un problème, car ce type d’équipement est désormais largement disponible. problème de deuxième et plus difficile Hello est que par étirement hello domaine d’erreur potentiel VLAN hello est étendue sites tooboth, essentiellement devient un point de défaillance unique. Bien que cela soit peu probable, il est arrivé qu’une tempête de diffusion commence, sans pouvoir être isolée. Sur ce dernier problème, les avis sont partagés. Nombre d’implémentations ont été réussies, tandis que des organisations ne souhaitent pas du tout entendre parler de cette technologie.
* Étendue de sous-réseau n’est pas possible si vous utilisez Microsoft Azure comme site de récupération d’urgence de hello.

### <a name="subnet-failover"></a>Basculement de sous-réseau
Il est possible tooimplement les avantages de solution de sous-réseau hello étirée décrite ci-dessus sans étirement de sous-réseau de hello sur plusieurs sites hello de la tooobtain de basculement de sous-réseau. Dans ce cas, n’importe quel sous-réseau donné serait présent sur le site 1 ou le site 2, mais jamais simultanément sur les deux sites. Dans l’ordre toomaintain hello espace d’adressage IP dans les événements hello d’un basculement, il est possible tooprogrammatically réorganiser des sous-réseaux de hello hello routeur infrastructure toomove à partir d’un site tooanother. Dans un Bonjour de scénario de basculement sous-réseaux sont déplacement par hello associés ordinateurs virtuels protégés. Hello principal inconvénient toothis consiste en cas de hello d’une panne avoir toomove hello sous-réseau entier, ce qui peut être OK, mais elle peut affecter les considérations relatives à la granularité hello basculement.

Nous allons examiner comment une entreprise fictive nommée Contoso est tooreplicate en mesure de son emplacement de récupération tooa machines virtuelles pendant le basculement de sous-réseau en entier hello. Nous allons tout d’abord examiner comment Contoso est en mesure de toomanage leurs sous-réseaux tandis que la réplication des machines virtuelles entre deux local emplacements, puis nous aborderons basculement de sous-réseaux fonctionne quand [Azure est utilisé comme site de récupération d’urgence hello](#failover-to-azure).

#### <a name="failover-from-on-premises-tooazure"></a>Basculement local tooAzure 
Azure Site Recovery (ASR) permet à Azure toobe utilisé comme un site de récupération d’urgence pour vos ordinateurs virtuels.  

Examinons un scénario dans lequel la société fictive Woodgrove Bank dispose d’une infrastructure locale, qui héberge ses applications métier, et d’Azure qui héberge ses applications mobiles. La connectivité entre les machines virtuelles de la Woodgrove Bank dans Azure et les serveurs locaux est assurée par un réseau privé virtuel de site à site ou ExpressRoute. Les VPN S2S permet de réseau virtuel de Woodgrove Bank dans Azure toobe considéré comme une extension de la Woodgrove Bank réseau sur site. Cette communication est permise par le réseau privé virtuel de site à site entre le périmètre de la Woodgrove Bank et le réseau virtuel Azure. Woodgrove veut maintenant toouse ASR tooreplicate sa région Azure principale tooanother région Azure en cours d’exécution de charges de travail. Cette option répond aux besoins de hello Woodgrove, ce qui veut une option de récupération d’urgence économique et est en mesure de toostore des données dans les environnements de cloud public. Woodgrove a toodeal avec les applications et les configurations varie en fonction des adresses IP codées en dur, par conséquent, ils ont une exigence tooretain IP des adresses pour leurs applications après un échec de région tooanother dans Azure.

Woodgrove a décidé tooassign des adresses IP à partir des ressources de tooits plage (172.16.1.0/24, 172.16.2.0/24) adresse IP en cours d’exécution dans Azure.

Pour tooreplicate en mesure de Woodgrove toobe son tooAzure de machines virtuelles tout en conservant les adresses IP hello, un réseau virtuel Azure doit toobe créé. Il doit être une extension du réseau local de hello pour que les applications puissent basculer de hello local site tooAzure en toute transparence. Azure vous permet de tooadd site à site, ainsi que des point-to-site VPN connectivité toohello réseaux virtuels créés dans Azure. Lorsque vous configurez votre connexion de site à site, réseau Azure vous permet d’emplacement de site tooroute trafic toohello (Azure appelle réseau local) uniquement si la plage d’adresses IP hello est différent de la plage d’adresses IP locales hello, car Azure ne prise en charge l’étirement des sous-réseaux.  Cela signifie que si vous avez un 192.168.1.0/24 sous-réseau local, vous ne pouvez pas ajouter un réseau local de 192.168.1.0/24 Bonjour réseau Azure. Ceci est dû au fait que Azure ne sait pas qu’il en existe aucune machine virtuelle active dans le sous-réseau de hello et sous-réseau hello est créé uniquement à des fins de récupération d’urgence. toobe toocorrectly en mesure de router le trafic réseau en dehors d’un Azure hello des sous-réseaux dans le réseau de hello et réseau local hello ne doit pas entrer en conflit.

![Avant le basculement de sous-réseau](./media/site-recovery-network-design/network-design7.png)

Avant le basculement

toohelp Woodgrove répondre aux besoins de leur entreprise, nous devons hello tooimplement suivant du flux de travail :

* Créer un réseau supplémentaire, appelez-la récupération réseau, où les ordinateurs virtuels ayant basculé hello serait créés.
* tooensure que IP hello pour une machine virtuelle est conservée après un basculement, passez l’onglet configurer de toohello sous propriétés de la machine virtuelle, spécifiez les hello même adresse IP qui hello machine virtuelle a local, puis cliquez sur Enregistrer. Lorsque hello machine virtuelle est basculé, Azure Site Recovery attribuera hello IP toohello virtual machine fournie.

![Propriétés du réseau](./media/site-recovery-network-design/network-design8.png)

Une fois hello de basculement est déclenché et hello virtuels sont créés dans hello réseau de récupération avec adresse IP hello souhaité, toothis de connectivité réseau est établie à l’aide un [tooVnet de réseau virtuel connexion](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md). Si nécessaire, cette action peut faire l’objet d’un script.  Comme expliqué dans la section précédente de hello sur le basculement de sous-réseau, même dans les cas de hello de basculement tooAzure, itinéraires serait ont toobe modifiées en conséquence tooreflect que 192.168.1.0/24 a déplacé maintenant tooAzure.

![Après le basculement de sous-réseau](./media/site-recovery-network-design/network-design9.png)

Après le basculement

Si vous n’avez un réseau « Azure » comme indiqué dans l’image hello ci-dessus. Vous pouvez créer un réseau VPN site toosite entre votre « Site principal » et une « Récupération réseau » après le basculement de hello.  


#### <a name="failover-tooa-secondary-on-premises-site"></a>Tooa basculement secondaire site local
Examinons un scénario où nous souhaitons conserver IP hello de chacune des machines virtuelles de hello et basculement hello effectuer sous-réseau ensemble. site principal de Hello possède des applications en cours d’exécution dans le sous-réseau 192.168.1.0/24. En cas de basculement de hello, tous les ordinateurs virtuels hello qui font partie de ce sous-réseau doit être effectués à un site de récupération toohello et conservent leurs adresses IP. Itinéraires aura toobe fait de hello tooreflect que tous les ordinateurs virtuels de hello appartenant toosubnet 192.168.1.0/24 ont été déplacés de site de récupération toohello modifiées en conséquence.

Bonjour suivant hello d’illustration achemine entre le site principal et le site de récupération, site tiers et site principal, et troisième site et le site de récupération auront toobe modifiée en conséquence.

Hello suivant images montre les sous-réseaux hello avant le basculement de hello. Sous-réseau 192.168.0.1/24 est active sur hello Site principal avant le basculement de hello et devient active de hello Site de récupération après un basculement de hello

![Avant le basculement](./media/site-recovery-network-design/network-design2.png)

Avant le basculement

image Hello ci-dessous montre les réseaux et les sous-réseaux après le basculement.

![Après le basculement](./media/site-recovery-network-design/network-design3.png)

Après le basculement

Dans votre site secondaire soit en local et que vous utilisez un toomanage du serveur VMM ensuite lorsque activation de la protection pour un ordinateur virtuel spécifique, ASR alloue des ressources réseau en fonction de toohello suivant du flux de travail :

* Récupération automatique du système alloue une adresse IP pour chaque interface réseau sur l’ordinateur virtuel de hello hello statique pool d’adresses IP définie sur le réseau approprié de hello pour chaque instance de System Center VMM.
* Si l’administrateur de hello définit hello IP même pool pour le réseau hello sur le site de récupération hello en tant que d’adresses qu’affecte du pool d’adresses IP hello Hello réseau sur le site principal hello, lors de l’allocation hello IP adresse toohello réplica machine virtuelle ASR hello même Adresse IP que celle de l’ordinateur virtuel principal hello.  Hello IP est réservée dans VMM, mais pas défini en tant qu’IP de basculement sur l’ordinateur hôte Hyper-v de hello. Failover IP sur un ordinateur hôte Hyper-v est définie juste avant le basculement de hello.


Si hello même adresse IP n’est pas disponible, ASR affecte une autre adresse IP disponible du pool d’adresses IP hello défini.

Après avoir hello que machine virtuelle est activée pour la protection, vous pouvez utiliser suivant exemple script tooverify hello IP qui a été alloué toohello virtual machine. Hello serait définir en tant que Failover IP et affecté toohello machine virtuelle au moment du basculement de hello même adresse IP :

        $vm = Get-SCVirtualMachine -Name <VM_NAME>
        $na = $vm[0].VirtualNetworkAdapters>
        $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
        $ip.address  

> [!NOTE]
> Dans le scénario de hello dans lequel les machines virtuelles utilisent DHCP, gestion hello des adresses IP est entièrement en dehors du contrôle hello de récupération automatique du système. Un administrateur a tooensure hello DHCP à servir hello adresses IP de serveur sur site de récupération hello peuvent faire Office de hello même plage que celle du site principal de hello.
>
>



## <a name="option-2-changing-ip-addresses"></a>Option 2 : modification des adresses IP
Cette approche paraît hello toobe prédominant en fonction de ce que nous l’avons vu. Il prend le formulaire hello du changement d’adresse IP de hello de chaque machine virtuelle qui est impliqué dans le basculement hello. L’inconvénient de cette approche nécessite hello entrants réseau too'learn' application hello au IPx est désormais à IPy. Même si IPx et IPy sont des noms logiques, des entrées DNS ont généralement toobe modifié ou vidé réseau de hello et des entrées mises en cache dans les tables de réseau ont toobe mis à jour ou vidés, par conséquent, un temps d’arrêt peut se produire en fonction de l’infrastructure DNS hello dispose de la été le programme d’installation. Ces problèmes peuvent être atténuées en utilisant les valeurs de durée de vie faibles dans les cas de hello d’applications intranet et [Azure Traffic Manger avec ASR](http://azure.microsoft.com/blog/2015/03/03/reduce-rto-by-using-azure-traffic-manager-with-azure-site-recovery/) applications basées sur Internet

### <a name="changing-hello-ip-addresses---illustration"></a>La modification des adresses IP hello - Illustration
Examinons le scénario de hello lorsque vous prévoyez de toouse différentes adresses IP hello principal et les sites de récupération de hello. Bonjour à l’exemple suivant, nous avons également un site tiers où les applications hello hébergées sur le site principal ou de récupération sont accessibles.

![Autre adresse IP - avant le basculement](./media/site-recovery-network-design/network-design10.png)


Image hello ci-dessus, il existe certaines applications hébergées dans un sous-réseau 192.168.1.0/24 de sous-réseau sur le site principal de hello et qu’ils ont été configuré toocome sur le site de récupération hello dans le sous-réseau 172.16.1.0/24 après un basculement. Les itinéraires du réseau/des connexions VPN ont été correctement configurés pour que les trois sites puissent accéder l’un à l'autre.

En tant qu’image hello ci-dessous montre, après avoir basculé une ou plusieurs applications, ils seront restaurés dans le sous-réseau de récupération hello. Dans ce cas nous ne sommes pas contraint toofailover hello tout sous-réseau à hello même temps. Aucune modification n’est requis tooreconfigure les itinéraires VPN ou réseau. Un basculement et certaines mises à jour DNS garantissent le maintien de l’accessibilité des applications. Si hello DNS est configuré tooallow les mises à jour dynamiques virtuels hello serait inscrire eux-mêmes à l’aide de la nouvelle adresse IP de hello une fois qu’ils démarrent après un basculement.

![Autre adresse IP - après le basculement](./media/site-recovery-network-design/network-design11.png)


Une fois que l’ordinateur virtuel de réplica basculer hello peut avoir une adresse IP qui n’est pas identique hello en tant qu’adresse IP de hello de l’ordinateur virtuel principal hello. Machines virtuelles met à jour de serveur DNS hello qu’ils utilisent après leur démarrage. Les entrées DNS ont généralement toobe modifié ou vidé réseau hello, et des entrées mises en cache dans les tables de réseau ont toobe mis à jour ou vidé, il est donc pas rare toobe rencontré avec un temps mort alors que ces modifications ont lieu. Ce problème peut être atténué par :

* L’utilisation de valeurs TTL faibles pour les applications intranet.
* L’utilisation d’Azure Traffic Manager avec ASR pour les applications basées sur Internet.
* Utilisation de hello suit script au sein de la récupération du plan tooupdate hello serveur DNS tooensure une mise à jour en temps voulu (script de hello n’est pas requis si l’enregistrement DNS dynamique de hello est configuré)

        param(
        string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord

### <a name="changing-hello-ip-addresses--dr-tooazure"></a>Modification hello des adresses IP – tooAzure de récupération d’urgence
Hello [installation de l’Infrastructure réseau pour Microsoft Azure comme un Site de récupération d’urgence](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) billet de blog explique comment toosetup hello requis infrastructure de mise en réseau Azure lors de la conservation des adresses IP n’est pas obligatoire. Il commence par décrivant l’application hello et découvrir comment toosetup réseau local et sur Azure et concluant par la procédure toodo un test de basculement et un basculement planifié.

## <a name="next-steps"></a>Étapes suivantes
[En savoir plus](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) comment Site Recovery mappe les réseaux source et cible lorsque le site principal de hello toomanage utilisé est en cours d’un serveur VMM.
