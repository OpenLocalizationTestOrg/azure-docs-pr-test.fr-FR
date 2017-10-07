---
title: aaaCommon des questions sur Microsoft Azure Service Fabric | Documents Microsoft
description: "Questions fréquentes sur Service Fabric et leurs réponses"
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: 
ms.assetid: 5a179703-ff0c-4b8e-98cd-377253295d12
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: chackdan
ms.openlocfilehash: 4cbe92d2a03f7a1ea5d077807fdc982288220a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="commonly-asked-service-fabric-questions"></a>Questions fréquentes sur Service Fabric

Les utilisateurs posent fréquemment des questions sur l’utilisation et les fonctionnalités de Service Fabric. Ce document regroupe un grand nombre de ces questions fréquentes et leurs réponses.

## <a name="cluster-setup-and-management"></a>Création et gestion de clusters

### <a name="can-i-create-a-cluster-that-spans-multiple-azure-regions-or-my-own-datacenters"></a>Puis-je créer un cluster qui englobe plusieurs régions Azure ou mes propres centres de données ?

Oui. 

le cœur de Hello technologie de clustering de l’infrastructure de Service peut être utilisé toocombine machines exécutant n’importe où dans Bonjour, afin qu’ils ont tooeach de connectivité de réseau autre. Toutefois, la création et l’exécution d’un tel cluster peuvent être compliquées.

Si vous êtes intéressé par ce scénario, nous encourageons vous tooget en contact via hello [liste des problèmes Service Fabric Github](https://github.com/azure/service-fabric-issues) ou via votre représentant du support dans des instructions supplémentaires ordre tooobtain. équipe du Service Fabric Hello collabore tooprovide des précisions, instructions et recommandations pour ce scénario. 

Certains tooconsider choses : 

1. Hello du cluster Service Fabric dans Azure est régionaux aujourd'hui, comme le sont à l’échelle de machine virtuelle hello définit ce cluster hello repose sur. Cela signifie qu’en cas de hello d’une panne régionale vous risquez de perdre cluster de hello toomanage hello possibilité via hello Azure Resource Manager ou hello portail Azure. Cela peut se produire même si le cluster de hello reste en cours d’exécution et vous serez en mesure de toointeract avec lui directement. En outre, Azure aujourd'hui n’offre pas hello capacité toohave un seul réseau virtuel qui est utilisable dans différentes régions. Cela signifie qu’un cluster de plusieurs région dans Azure nécessite [des adresses IP publiques pour chaque machine virtuelle Bonjour jeux de mise à l’échelle de machine virtuelle](../virtual-machine-scale-sets/virtual-machine-scale-sets-networking.md#public-ipv4-per-virtual-machine) ou [les passerelles VPN Azure](../vpn-gateway/vpn-gateway-about-vpngateways.md). Toutes ces options de mise en réseau ont différents impacts sur les coûts, les performances et toosome degré design de l’application, une analyse minutieuse et planification est requis avant mettant un tel environnement.
2. Hello maintenance, la gestion et la surveillance de ces ordinateurs peuvent devenir complexes, en particulier lorsque fractionnés sur _types_ des environnements, tels qu’entre les fournisseurs de cloud différents ou entre des ressources locales et Azure . Soyez prudent tooensure qui met à niveau, l’analyse, gestion, et diagnostics sont compris pour le cluster de hello et applications de hello avant d’exécuter les charges de production dans un tel environnement. Si vous avez l’habitude de résoudre ces problèmes dans Azure ou dans vos propres centres de données, il est probable que vous puissiez appliquer ces mêmes solutions lors de la création ou de l’exécution de votre cluster Service Fabric. 

### <a name="do-service-fabric-nodes-automatically-receive-os-updates"></a>Les nœuds Service Fabric reçoivent-ils automatiquement les mises à jour du système d’exploitation ?

Pas aujourd'hui, mais il s’agit également d’une demande commune que Azure a l’intention toodeliver.

Bonjour temporaire, nous avons [fourni une application](service-fabric-patch-orchestration-application.md) que les systèmes d’exploitation hello sous les nœuds de l’infrastructure de Service restent corrigé et des toodate.

défi de Hello avec les mises à jour du système d’exploitation est qu’elles nécessitent généralement un redémarrage de l’ordinateur hello, ce qui entraîne une perte de disponibilité temporaire. Par lui-même, qui n’est pas un problème, étant donné que le Service Fabric redirige automatiquement le trafic pour les nœuds de tooother de services. Toutefois, si les mises à jour du système d’exploitation ne sont pas coordonnées sur le cluster de hello, il est risque de hello que plusieurs nœuds s’arrêtent en même temps. Ces redémarrages simultanés peuvent entraîner l’indisponibilité complète d’un service ou, au moins, d’une partition spécifique (pour un service avec état).

Bonjour future, nous prévoyons de stratégie de mise à jour toosupport un système d’exploitation qui est entièrement automatisée et la coordination entre les domaines de mise à jour, garantissant que la disponibilité est maintenue en dépit des redémarrages et d’autres défaillances inattendues.

### <a name="can-i-use-large-virtual-machine-scale-sets-in-my-sf-cluster"></a>Puis-je utiliser de grands groupes identiques de machines virtuelles dans mon cluster Service Fabric ? 

**Réponse courte** : Non. 

**Temps de réponse** - bien que les grands jeux de mise à l’échelle de Machine virtuelle hello vous permettent de tooscale une échelle de machines virtuelles définie jusqu'à 1000 les instances de machine virtuelle, il le fait à l’aide de hello de groupes de la sélection élective (pages). Domaines d’erreur (groupes) et mise à niveau (domaines d’erreur) sont uniquement cohérents au sein de la sélection élective groupe Service fabric utilise décisions de sélection élective toomake groupes et domaines d’erreur de vos instances de Service/réplicas de service. Étant donné que les groupes hello et les domaines d’erreur sont comparables uniquement dans un groupe de la sélection élective SF ne peut pas l’utiliser. Par exemple, si VM1 dans PG1 présente une topologie de FD = 0 et VM9 dans PG2 présente une topologie de FD = 4, cela ne signifie pas que VM1 et VM2 se trouvent sur deux Racks matériels différents, par conséquent SF Impossible d’utiliser les valeurs hello FD dans cette décisions de sélection élective toomake cas.

Il n’y autres problèmes liés à des machines virtuelles volumineux identiques, telles que la prise en charge de l’équilibrage de charge de manque de hello de niveau 4. Consultez toofor [plus d’informations sur la grande échelle jeux](../virtual-machine-scale-sets/virtual-machine-scale-sets-placement-groups.md)



### <a name="what-is-hello-minimum-size-of-a-service-fabric-cluster-why-cant-it-be-smaller"></a>Quelle est hello de taille minimale d’un cluster Service Fabric ? Pourquoi ne peut-il pas être plus petit ?

taille de prise en charge minimale Hello pour un cluster Service Fabric exécutant les charges de production est cinq nœuds. Pour les scénarios de développement/test, nous prenons en charge des clusters à trois nœuds.

Ces valeurs minimales existent, car le cluster Service Fabric de hello exécute un ensemble de services système avec état, y compris le service d’affectation de noms de hello et le Gestionnaire de basculement hello. Ces services, qui assurent le suivi de services ont été déploiement toohello cluster et où ils sont actuellement hébergés, dépendent de la cohérence forte. Sur la cohérence forte, à son tour, dépend de hello capacité tooacquire un *quorum* pour une mise à jour donnée état toohello de ces services, où un quorum représente une majorité stricte des réplicas hello (N/2 + 1) pour un service donné.

Dans ce cadre, examinons certaines configurations de cluster possibles :

**Un seul nœud**: cette option ne fournit pas de haute disponibilité, car la perte hello du nœud unique de hello pour une raison quelconque signifie une perte de hello de l’ensemble du cluster hello.

**Deux nœuds** : le quorum d’un service déployé sur deux nœuds (N = 2) est 2 (2/2 + 1 = 2). En cas de perte d’un seul réplica, il est impossible toocreate un quorum. Comme la mise à niveau d’un serveur requiert la mise hors ligne d’un réplica, cette configuration n’a aucune utilité.

**Trois nœuds**: trois nœuds (N = 3), hello exigence toocreate un quorum est toujours deux nœuds (3/2 + 1 = 2). Cela signifie que vous pouvez perdre un nœud et conserver le quorum.

configuration de cluster nœud trois Hello est pris en charge pour le développement et de test car vous pouvez en toute sécurité effectuer des mises à niveau et faire face aux défaillances de nœud individuel, tant qu’ils ne se produisent pas simultanément. Pour les charges de production, vous devez être résilient toosuch défaillance simultanée, cinq nœuds sont requis.

### <a name="can-i-turn-off-my-cluster-at-nightweekends-toosave-costs"></a>Puis-je désactiver mon cluster à des coûts toosave nuit/week-ends ?

En général, non. Service Fabric stocke l’état sur les disques locaux, éphémères, ce qui signifie que que si hello virtual machine est déplacé tooa autre ordinateur hôte, les données de salutation ne déplacement pas avec lui. En fonctionnement normal, qui n’est pas un problème comme nouveau nœud de hello est soulevé toodate par d’autres nœuds. Toutefois, si vous arrêtez tous les nœuds et les redémarrez ultérieurement, il est possible significatifs que la plupart des nœuds de hello démarre sur les nouveaux ordinateurs hôtes et toorecover impossible du système hello.

Si vous souhaitez que les clusters toocreate pour tester votre application avant son déploiement, nous vous recommandons de créer dynamiquement ces clusters dans le cadre de votre [intégration continu/continu pipeline de déploiement](service-fabric-set-up-continuous-integration.md).


### <a name="how-do-i-upgrade-my-operating-system-for-example-from-windows-server-2012-toowindows-server-2016"></a>Comment mettre à niveau mon système d’exploitation (par exemple à partir de Windows Server 2012 tooWindows Server 2016) ?

Pendant que nous recherchons une expérience améliorée, aujourd'hui, vous êtes responsable de la mise à niveau hello. Vous devez mettre à niveau image hello du système d’exploitation sur hello une machine virtuelle de cluster de machines virtuelles de hello à la fois. 

## <a name="container-support"></a>Support pour les conteneurs

### <a name="why-are-my-containers-that-are-deployed-toosf-unable-tooresolve-dns-addresses"></a>Pourquoi les mon conteneurs sont tooresolve Impossible de tooSF déployé DNS adresses ?

Ce problème a été signalé sur les clusters version 5.6.204.9494 

**Atténuation** : suivez [ce document](service-fabric-dnsservice.md) tooenable hello DNS du service service fabric dans votre cluster.

**Corriger** : version du cluster tooa mise à niveau pris en charge est supérieure à 5.6.204.9494, lorsqu’il est disponible. Si votre cluster tooautomatic les mises à niveau, puis les cluster hello met automatiquement à niveau version toohello qui possède cet correction du problème.

  
## <a name="application-design"></a>Conception des applications

### <a name="whats-hello-best-way-tooquery-data-across-partitions-of-a-reliable-collection"></a>Nouveautés hello meilleure façon tooquery que les données sur plusieurs partitions d’une Collection fiable

Collections fiables sont généralement [partitionnée](service-fabric-concepts-partitioning.md) tooenable montée en puissance parallèle pour les performances et le débit supérieur. Cela signifie qu’état hello pour un service donné peut-être être réparti sur 10 s ou 100 s des ordinateurs. tooperform des opérations sur ce jeu de données complet, vous disposez de plusieurs options :

- Créer un service qui interroge toutes les partitions d’un autre toopull de service dans les données de salutation requis.
- Créer un service capable de recevoir des données provenant de toutes les partitions d’un autre service.
- Transmettre des données à partir de chaque magasin externe de service tooan régulièrement. Cette approche n’est appropriée si vous effectuez une des requêtes hello ne font pas partie de votre logique d’entreprise.


### <a name="whats-hello-best-way-tooquery-data-across-my-actors"></a>Nouveautés hello meilleure façon tooquery que les données sur mon acteurs

Acteurs sont conçus toobe des unités indépendantes de l’état et calcul, donc il n’est pas recommandé tooperform grandes requêtes d’état d’acteur lors de l’exécution. Si vous avez un besoin tooquery ensemble complet de hello d’état d’acteur, vous devez envisager soit :

- Remplacement de vos services d’acteur avec des services fiables avec état, telles que nombre hello du réseau demande toogather toutes les données à partir du numéro de hello du toohello acteurs de partitions dans votre service.
- Conception de votre publication de tooperiodically acteurs leur tooan externe le magasin d’état pour les requêtes plus faciles. Comme ci-dessus, cette approche n’est viable que si vous effectuez une des requêtes hello ne sont pas requises pour votre comportement d’exécution.

### <a name="how-much-data-can-i-store-in-a-reliable-collection"></a>Quelle quantité de données puis-je stocker dans une collection fiable ?

Services fiables sont généralement partitionnées, hello quantité que vous pouvez stocker est uniquement limitée par nombre de hello d’ordinateurs que vous disposez dans le cluster de hello et hello quantité de mémoire disponible sur ces ordinateurs.

Par exemple, supposons que vous ayez une collection fiable dans un service de 100 partitions et 3 réplicas, la taille moyenne des objets stockés est de 1 Ko. Maintenant, supposons que vous disposiez d’un cluster de 10 ordinateurs avec 16 Go de mémoire par ordinateur. Pour plus de simplicité et toobe très classique, supposons que hello système d’exploitation et les services système, hello Service Fabric runtime et vos services exigent 6 Go, en laissant 10 Go disponibles par ordinateur ou 100 Go pour le cluster de hello.

Sachant que chaque objet doit être stocké trois fois (une copie principale et deux réplicas), vous aurez suffisamment de mémoire pour environ 35 millions d’objets dans votre collection lorsqu’elle fonctionnera à pleine capacité. Toutefois, nous vous recommandons d’être résilient toohello la perte simultanée d’un domaine de défaillance et un domaine de mise à niveau, ce qui représente environ 1/3 de la capacité et réduit de manière tooroughly de nombre hello 23 millions.

Notez que ce calcul suppose également :

- Cette distribution hello des données entre les partitions hello est à peu près uniforme ou que vous rencontrez des métriques de charge toohello Gestionnaire de ressources du Cluster. Par défaut, Service Fabric équilibre la charge en fonction du nombre de réplicas. Dans notre exemple ci-dessus, qui place les réplicas principales 10 et 20 secondaire sur chaque nœud de cluster de hello. Qui fonctionne bien pour la charge est répartie équitablement entre les partitions hello. Si la charge n’est pas encore, vous devez indiquez charge afin qu’hello Gestionnaire de ressources peut pack ensemble de réplicas plus petits et autoriser supérieure réplicas tooconsume davantage de mémoire sur un nœud individuel.

- Ce service fiable hello en question est le seul état stockage hello dans un cluster de hello. Étant donné que vous pouvez déployer plusieurs clusters tooa de services, vous devez toobe penser ressources hello que chacune sera peut-être toorun et gérer son état.

- Ce cluster hello lui-même n’est pas agrandissement ou la réduction. Si vous ajoutez plusieurs ordinateurs, Service Fabric rééquilibrer les vos réplicas tooleverage hello une capacité supplémentaire tant que nombre hello d’ordinateurs dépasse le nombre hello de partitions dans votre service, car un réplica individuel ne peut pas s’étendre sur des ordinateurs. En revanche, si vous réduisez la taille de hello du cluster de hello en supprimant les ordinateurs, vos réplicas seront compressés plus étroitement et comportent moins de capacité globale.

### <a name="how-much-data-can-i-store-in-an-actor"></a>Quelle quantité de données puis-je stocker dans un acteur ?

Comme avec les services fiables, hello quantité de données que vous pouvez stocker dans un service d’acteur est uniquement limitée par hello sur le disque et de mémoire disponible sur les nœuds hello dans votre cluster. Toutefois, les acteurs individuels sont plus efficaces lorsqu’ils sont utilisé tooencapsulate une petite quantité de logique métier associée et l’état. En règle générale, un acteur doit avoir l’état qui est mesuré en kilo-octets.

## <a name="other-questions"></a>Autres questions

### <a name="how-does-service-fabric-relate-toocontainers"></a>Comment Service Fabric liée toocontainers ?

Les conteneurs offrent un moyen simple toopackage services et leurs dépendances tels qu’ils exécuter cohérente dans tous les environnements et peuvent fonctionner de manière isolée sur un seul ordinateur. L’infrastructure de service offre un moyen toodeploy et gérer des services, y compris [services empaquetées dans un conteneur](service-fabric-containers-overview.md).

### <a name="are-you-planning-tooopen-source-service-fabric"></a>Envisagez-vous tooopen source Service Fabric ?

Nous avez l’intention des services fiables tooopen source hello et infrastructures d’acteurs fiable sur GitHub et acceptera des projets de communautés contributions toothose. Veuillez suivre hello [Service Fabric blog](https://blogs.msdn.microsoft.com/azureservicefabric/) pour plus d’informations, comme ils sont annoncés.

Hello n’existe actuellement aucune exécution de plans tooopen source hello Service Fabric.

## <a name="next-steps"></a>Étapes suivantes

- [En savoir plus sur les principaux concepts et les meilleures pratiques de Service Fabric](https://mva.microsoft.com/en-us/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965)
