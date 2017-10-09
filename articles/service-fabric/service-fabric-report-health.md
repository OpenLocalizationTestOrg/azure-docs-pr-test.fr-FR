---
title: "rapports d’intégrité de l’infrastructure de Service personnalisés aaaAdd | Documents Microsoft"
description: "Décrit comment les rapports d’état personnalisé toosend entités de contrôle d’intégrité tooAzure Service Fabric. Fournit des recommandations pour la conception et la mise en œuvre de rapports d’intégrité de qualité."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 0a00a7d2-510e-47d0-8aa8-24c851ea847f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: oanapl
ms.openlocfilehash: 12c9f664e2a457b4e1e8f340873ca60ebcefb097
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-service-fabric-health-reports"></a>Ajout de rapports d’intégrité Service Fabric personnalisés
Azure Service Fabric introduit un [modèle d’intégrité](service-fabric-health-introduction.md) conçu tooflag les cluster défectueux et les conditions d’application sur des entités spécifiques. modèle de contrôle d’intégrité Hello utilise **rapporteurs de contrôle d’intégrité** (composants système et des agents de surveillance). objectif de Hello est facile et rapide de diagnostic et de réparation. Enregistreurs de service doivent toothink dès le départ sur le contrôle d’intégrité. Toutes les conditions qui peuvent avoir un impact sur l’intégrité doivent être signalée, surtout si elle peut aider à des problèmes d’indicateur fermer toohello racine. informations de contrôle d’intégrité Hello pouvant gagner du temps sur l’examen et le débogage. Hello utilité est particulièrement évident une fois hello service en cours d’exécution à grande échelle dans le cloud de hello (privée ou Azure).

Moniteur de rapporteurs Hello Service Fabric identifié les conditions d’intérêt. Ils dressent un rapport sur ces conditions en fonction de leur vue locale. Hello [magasin de contrôle d’intégrité](service-fabric-health-introduction.md#health-store) agrège des données de contrôle d’intégrité envoyées par tous les rapporteurs toodetermine si les entités sont globalement intègres. modèle de Hello est toouse riche, flexible et facile de toobe prévue. qualité Hello de rapports d’intégrité de hello détermine la précision hello de vue de contrôle d’intégrité hello du cluster de hello. Des faux positifs qui indiquent erronément des problèmes d’intégrité peuvent avoir une incidence négative sur les mises à niveau ou autres services utilisant des données d’intégrité. Les services de réparation et mécanismes d’alertes sont des exemples de services de ce type. Par conséquent, la réflexion est rapports tooprovide nécessaires qui capturent les conditions d’intérêt dans hello meilleure façon possible.

toodesign et mettre en œuvre l’intégrité reporting, agents de surveillance et les composants système doivent :

* Définir la condition hello qu'intéressent, moyen hello qu'il est analysé et hello a d’impact sur la fonctionnalité de cluster ou une application hello. En fonction de ces informations, décider de hello rapport d’intégrité et de la propriété état d’intégrité.
* Déterminer hello [entité](service-fabric-health-introduction.md#health-entities-and-hierarchy) que hello état s’applique.
* Déterminer où hello reporting est effectuée, depuis hello surveillance de service ou à partir d’une commande interne ou externe.
* Définir un rapporteur de hello tooidentify source utilisée.
* Choisir une stratégie de création de rapports, périodiquement ou selon les transitions. Hello recommandé consiste régulièrement, car elle nécessite que du code plus simple et est moins sujet tooerrors.
* Déterminer les rapports hello combien de temps pour les conditions non intègres doivent rester dans le magasin de contrôle d’intégrité hello et comment il doit être effacé. À l’aide de ces informations, de déterminer le comportement au moment de l’état hello toolive et suppression à l’expiration.

Comme mentionné auparavant, la création de rapports peut être effectuée à partir des éléments suivants :

* Hello analysés réplica de service Service Fabric.
* Les agents de surveillance internes déployés en tant que services Service Fabric (par exemple, un service Service Fabric sans état, qui surveille des conditions et émet des rapports). agents de surveillance Hello peuvent être déployé une tous les nœuds ou peuvent être associés toohello analysé service.
* Agents de surveillance internes qui s’exécutent sur des nœuds de Service Fabric hello mais sont *pas* implémenté en tant que services de Fabric de Service.
* Externe watchdogs cette ressource hello de sonde de *en dehors de* cluster Service Fabric de hello (par exemple, service de surveillance comme Gomez).

> [!NOTE]
> En dehors de la zone de hello, cluster de hello est remplie avec les rapports d’intégrité envoyés par les composants du système hello. Pour en savoir plus, voir [Utilisation des rapports d’intégrité système pour la résolution des problèmes](service-fabric-understand-and-troubleshoot-with-system-health-reports.md). Hello rapports utilisateur doivent être envoyés [les entités d’intégrité](service-fabric-health-introduction.md#health-entities-and-hierarchy) qui ont déjà été créés par le système de hello.
> 
> 

Une fois hello design de création de rapports d’intégrité est clair, rapports d’intégrité peuvent être envoyés facilement. Vous pouvez utiliser [fabricclient ne](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) tooreport intégrité si hello cluster n’est pas [sécurisé](service-fabric-cluster-security.md) ou si le client de l’ensemble fibre optique hello a des privilèges d’administrateur. Création de rapports peut être effectuée via hello API par à l’aide de [FabricClient.HealthManager.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth), PowerShell, ou via REST. Des boutons de configuration regroupent les rapports afin d’améliorer les performances.

> [!NOTE]
> Signalement d’intégrité est synchrone, et il représente uniquement les travaux de validation hello côté client de hello. fait que hello rapport Hello est accepté par le client de contrôle d’intégrité de hello ou hello `Partition` ou `CodePackageActivationContext` objets ne signifie pas qu’il est appliqué dans le magasin de hello. Il est envoyé de manière asynchrone et éventuellement regroupé avec d’autres rapports. Hello traitement sur le serveur de hello peut-être encore échouer : numéro de séquence hello peut être périmé, entité hello sur quel hello rapport doit être appliqué a été supprimé, etc..
> 
> 

## <a name="health-client"></a>Client de contrôle d’intégrité
rapports d’intégrité de Hello sont envoyés magasin de contrôle d’intégrité toohello via un client de contrôle d’intégrité, qui se trouve à l’intérieur du client de l’ensemble fibre optique hello. client de contrôle d’intégrité Hello peut être configuré avec hello suivant les paramètres :

* **HealthReportSendInterval**: délai hello entre le rapport de hello temps hello est ajouté toohello client et hello le temps qu’il est envoyé le magasin de contrôle d’intégrité toohello. Rapports toobatch utilisé dans un seul message, plutôt que d’envoyer un message pour chaque rapport. le traitement par lot Hello améliore les performances. Par défaut : 30 secondes.
* **HealthReportRetrySendInterval**: magasin de contrôle d’intégrité toohello des rapports intervalle hello à quels hello client de contrôle d’intégrité renvoie le cumul d’intégrité. Par défaut : 30 secondes.
* **HealthOperationTimeout**: délai d’attente hello pour un message de rapport envoyé le magasin de contrôle d’intégrité toohello. Si un message arrive à expiration, client de contrôle d’intégrité hello réessaie jusqu'à ce que le magasin de contrôle d’intégrité hello confirme que le rapport de hello a été traitée. Par défaut : deux minutes.

> [!NOTE]
> Lorsque les rapports hello sont traités par lot, les clients de l’ensemble fibre optique hello doivent être maintenus actifs au moins hello tooensure HealthReportSendInterval qui leur sont envoyés. Si le message de type hello est perdu ou magasin de contrôle d’intégrité hello ne peut pas les appliquer en raison d’erreurs de tootransient, client de l’ensemble fibre optique hello doit rester actif toogive plus de temps il un tooretry chance.
> 
> 

Hello mise en mémoire tampon sur le client de hello prend l’unicité de hello des rapports de hello en considération. Par exemple, si un rapporteur incorrect particulier ne signale pas 100 rapports par seconde sur hello même propriété Hello même entité, hello rapports sont remplacées par la dernière version de hello. Au plus un rapport de ce type existe dans la file d’attente du client hello. Si le traitement par lot est configurée, hello d’états envoyés magasin de contrôle d’intégrité toohello est qu’une seule par intervalle d’envoi. Ce rapport est hello dernier ajout de rapports, qui reflète l’état le plus récent de l’entité de hello hello.
Spécifiez les paramètres de configuration lorsque `FabricClient` est créé en passant [FabricClientSettings](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclientsettings) avec hello valeurs souhaitées pour les entrées relatives à la santé.

Bonjour exemple suivant crée un client de l’ensemble fibre optique et spécifie que les rapports hello doivent être envoyés lorsqu’ils sont ajoutés. En cas de délais d’attente et d’erreurs pouvant donner lieu à une nouvelle tentative, les nouvelles tentatives ont lieu toutes les 40 secondes.

```csharp
var clientSettings = new FabricClientSettings()
{
    HealthOperationTimeout = TimeSpan.FromSeconds(120),
    HealthReportSendInterval = TimeSpan.FromSeconds(0),
    HealthReportRetrySendInterval = TimeSpan.FromSeconds(40),
};
var fabricClient = new FabricClient(clientSettings);
```

Nous recommandons de conserver l’ensemble fibre optique de hello par défaut des paramètres de client, définissent `HealthReportSendInterval` too30 secondes. Ce paramètre permet de garantir des performances optimales toobatching échéance. Pour les rapports critiques qui doivent être envoyés dès que possible, utilisez `HealthReportSendOptions` avec Immediate `true` dans l’API [FabricClient.HealthClient.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth). Rapports immédiates contournement hello intervalle de traitement par lot. Utilisez cet indicateur avec précaution ; Nous souhaitons parti tootake du client de contrôle d’intégrité hello le traitement par lots chaque fois que possible. Envoi immédiat est également utile lors de la fermeture de client de l’ensemble fibre optique hello (par exemple, les processus hello a déterminé l’état non valide et doit tooshut tooprevent effets vers le bas). Elle garantit un envoi meilleur effort des rapports de hello accumulée. Lorsqu’un rapport est ajouté avec l’indicateur immédiate, client de contrôle d’intégrité hello traite tous les rapports hello accumulée depuis le dernier envoi.

Mêmes paramètres peuvent être spécifiés lors de la création d’un cluster de tooa connexion via PowerShell. Bonjour à l’exemple suivant démarre un cluster local tooa de connexion :

```powershell
PS C:\> Connect-ServiceFabricCluster -HealthOperationTimeoutInSec 120 -HealthReportSendIntervalInSec 0 -HealthReportRetrySendIntervalInSec 40
True

ConnectionEndpoint   :
FabricClientSettings : {
                       ClientFriendlyName                   : PowerShell-1944858a-4c6d-465f-89c7-9021c12ac0bb
                       PartitionLocationCacheLimit          : 100000
                       PartitionLocationCacheBucketCount    : 1024
                       ServiceChangePollInterval            : 00:02:00
                       ConnectionInitializationTimeout      : 00:00:02
                       KeepAliveInterval                    : 00:00:20
                       HealthOperationTimeout               : 00:02:00
                       HealthReportSendInterval             : 00:00:00
                       HealthReportRetrySendInterval        : 00:00:40
                       NotificationGatewayConnectionTimeout : 00:00:00
                       NotificationCacheUpdateTimeout       : 00:00:00
                       }
GatewayInformation   : {
                       NodeAddress                          : localhost:19000
                       NodeId                               : 1880ec88a3187766a6da323399721f53
                       NodeInstanceId                       : 130729063464981219
                       NodeName                             : Node.1
                       }
```

De même tooAPI, les rapports peuvent être envoyés à l’aide de `-Immediate` commutateur toobe envoyé immédiatement, quelle que soit hello `HealthReportSendInterval` valeur.

Pour REST, hello rapports sont envoyés passerelle toohello Service Fabric, ce qui a un client de l’infrastructure interne. Par défaut, ce client est configuré toosend les rapports traités par lot toutes les 30 secondes. Vous pouvez modifier l’intervalle de lot hello avec le paramètre de configuration de cluster hello `HttpGatewayHealthReportSendInterval` sur `HttpGateway`. Comme mentionné, il vaut mieux toosend des rapports hello avec `Immediate` true. 

> [!NOTE]
> tooensure non autorisée de services ne peut pas rapporter d’intégrité sur des entités hello dans un cluster de hello, configurer hello server tooaccept uniquement les demandes provenant des clients sécurisés. Hello `FabricClient` utilisé pour la création de rapports doit avoir sécurité activée toocommunicate en mesure de toobe avec cluster hello (par exemple, avec l’authentification Kerberos ou certificat). En savoir plus sur la [sécurité du cluster](service-fabric-cluster-security.md).
> 
> 

## <a name="report-from-within-low-privilege-services"></a>Création de rapports depuis les services à faibles privilèges
Si les services de Fabric de Service n’ont pas de cluster de toohello d’accès administrateur, vous pouvez signaler d’intégrité sur les entités à partir du contexte actuel de hello via `Partition` ou `CodePackageActivationContext`.

* Pour les services sans état, utilisez [IStatelessServicePartition.ReportInstanceHealth](https://docs.microsoft.com/dotnet/api/system.fabric.istatelessservicepartition.reportinstancehealth) tooreport sur l’instance actuelle du service hello.
* Pour les services avec état, utilisez [IStatefulServicePartition.ReportReplicaHealth](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition.reportreplicahealth) tooreport sur le réplica en cours.
* Utilisez [IServicePartition.ReportPartitionHealth](https://docs.microsoft.com/dotnet/api/system.fabric.iservicepartition.reportpartitionhealth) tooreport sur l’entité de partition actuel hello.
* Utilisez [CodePackageActivationContext.ReportApplicationHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportapplicationhealth) tooreport sur l’application actuelle.
* Utilisez [CodePackageActivationContext.ReportDeployedApplicationHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportdeployedapplicationhealth) tooreport dans l’application actuelle hello déployée sur le nœud actuel de hello.
* Utilisez [CodePackageActivationContext.ReportDeployedServicePackageHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportdeployedservicepackagehealth) tooreport sur un package de service pour l’application hello déployé sur le nœud actuel de hello.

> [!NOTE]
> En interne, hello `Partition` et hello `CodePackageActivationContext` contenir un client de contrôle d’intégrité configuré avec les paramètres par défaut. Comme expliqué pourquoi [client de contrôle d’intégrité](service-fabric-report-health.md#health-client), les rapports sont traités par lot et envoyés sur un minuteur. les objets Hello doivent être conservés toohave actif à un rapport de hello toosend chance.
> 
> 

Vous pouvez spécifier `HealthReportSendOptions` lors de l’envoi de rapports par le biais des API de contrôle d’intégrité `Partition` et `CodePackageActivationContext`. Si des rapports critiques doivent être envoyés dès que possible, utilisez `HealthReportSendOptions` avec Immediate `true`. Rapports immédiates contournement hello intervalle du client de contrôle d’intégrité interne hello de traitement par lot. Comme mentionné précédemment, utilisez-le avec précaution ; Nous souhaitons parti tootake du client de contrôle d’intégrité hello le traitement par lots chaque fois que possible.

## <a name="design-health-reporting"></a>Conception de rapports d’intégrité
Hello première étape de génération de rapports de haute qualité est l’identification des conditions de hello pouvant affecter intégrité hello du service de hello. Toutes les conditions qui peuvent aider à des problèmes d’indicateur dans le cluster ou le service de hello lors du démarrage, ou mieux encore, avant un problème se produit, peut éventuellement enregistrer milliards de dollars. Hello avantages inférieur temps d’arrêt, le moins d’heures nuit consacré à examiner et réparer les problèmes et la satisfaction des clients plus élevée.

Une fois que les conditions de hello sont identifiées, les enregistreurs de surveillance doivent toofigure des meilleures toomonitor de façon hello pour trouver un équilibre entre la charge et de l’utilité. Prenons comme exemple un service qui effectue des calculs complexes qui utilisent des fichiers temporaires sur un partage. Une surveillance peut surveiller hello tooensure de partage que l’espace est suffisant. Il peut écouter les notifications relatives aux modifications de fichiers ou de répertoires. Il peut signaler un avertissement si un seuil initial est atteint et signale une erreur si le partage de hello est plein. Un avertissement, un système de réparation a pu démarrer nettoyage des anciens fichiers sur le partage de hello. En cas d’erreur, un système de réparation peut déplacer nœud tooanother de hello service réplica. Notez comment les États de condition hello sont décrits en termes de contrôle d’intégrité : hello état de hello condition peut être considéré comme saine (OK) ou défectueux (avertissement ou erreur).

Une fois les détails de surveillance hello définies, un writer de surveillance doit toofigure out comment tooimplement hello surveillance. Si les conditions hello peuvent être déterminées à partir de service de hello, surveillance de hello peut faire partie du service hello analysé lui-même. Par exemple, code de service hello peut vérifier l’utilisation du partage hello et puis chaque fois qu’il tente de toowrite un fichier de rapport. avantage Hello de cette approche est que la création de rapports est simple. Il convient de tooprevent les bogues de surveillance d’affecter les fonctionnalités d’un service hello.

Création de rapports à partir de service de hello analysé n’est pas toujours une option. Une surveillance au sein du service de hello peut-être pas les conditions de hello toodetect en mesure de. Il ne peut pas avoir détermination de hello toomake logique ou les données des hello. surcharge de Hello de surveillance des conditions de hello peut être élevé. conditions de Hello également peuvent ne pas être spécifique tooa service, mais au lieu de cela affecter les interactions entre les services. Une autre option consiste toohave des agents de surveillance dans un cluster de hello en tant que processus distincts. agents de surveillance Hello surveiller des conditions de hello et les rapports, sans affecter les principaux services de hello en aucune façon. Par exemple, ces agents de surveillance peuvent être implémentées en tant que services sans état Bonjour même application, déployée sur tous les nœuds ou hello mêmes nœuds en tant que service de hello.

Parfois, une surveillance en cours d’exécution dans un cluster de hello n’est pas une option soit. Si condition de hello analysé disponibilité de hello ou des fonctionnalités du service de hello comme les utilisateurs le voir, il s’agit meilleures agents de surveillance de hello toohave Bonjour même endroit en tant que clients utilisateur hello. Là, ils peuvent tester le fonctionnement de hello Bonjour d’utilisateurs les appellent. Par exemple, vous pouvez avoir une surveillance qui réside en dehors du cluster de hello et émet des requêtes toohello service vérifie la latence de hello et l’exactitude des résultats de hello. (Par exemple, pour un service de calculatrice, l’opération 2 + 2 retourne-t-elle 4 dans un délai raisonnable ?)

Une fois que les détails de surveillance hello ont été finalisées, vous devez choisir un ID de source qui identifie de façon unique. Si plusieurs agents de surveillance de hello même type sont courantes dans hello cluster, ils doivent créer un rapport sur les différentes entités, ou, si ceux-ci font sur hello même entité, utiliser l’ID source différente ou propriété. De cette façon, leurs rapports peuvent coexister. propriété Hello du rapport de contrôle d’intégrité hello doit capturer la condition de hello analysé. (Pour l’exemple hello ci-dessus, la propriété de hello peut être **ShareSize**.) Si plusieurs rapports appliquent toohello même condition, hello propriété doit contenir des informations dynamiques que toocoexist de rapports. Par exemple, si plusieurs partages doivent toobe analysé, nom de la propriété hello peut être **ShareSize-nom_partage**.

> [!NOTE]
> Faire *pas* utiliser hello magasin tookeep informations d’état. Seules les informations relatives à la santé doivent être signalées comme contrôle d’intégrité, en tant que cette évaluation de l’intégrité des informations impacts hello d’une entité. magasin de contrôle d’intégrité Hello n’est pas conçu comme un magasin à usage général. Il utilise tooaggregate de logique d’évaluation d’intégrité de toutes les données dans l’état d’intégrité hello. Envoi d’informations toohealth non liée (par exemple, signalent l’état de l’état d’intégrité de OK) n’affecte pas la hello agrégées à l’état d’intégrité, mais il peut nuire aux performances hello du magasin de contrôle d’intégrité hello.
> 
> 

point de décision suivant Hello est le tooreport entité sur. La plupart du temps hello, condition de hello clairement idetifies hello d’entité. Choisissez l’entité de hello avec une meilleure granularité possible. Si une condition a une incidence sur tous les réplicas d’une partition, un rapport sur la partition de hello, pas sur le service de hello. Il existe cependant des cas où une réflexion approfondie s’impose. Si la condition de hello a une incidence sur une entité, comme un réplica, mais hello désir est toohave hello condition marquée plus longtemps que la durée de hello de durée de vie de réplica, puis il doit être signalée sur la partition de hello. Dans le cas contraire, lorsque le réplica de hello est supprimé, magasin de contrôle d’intégrité hello nettoie tous ses rapports. Les enregistreurs de surveillance doivent penser à la durée de vie hello d’entité de hello et rapport de hello. Le moment où un rapport doit être effacé d’un magasin doit être clair (par exemple, lorsqu’une erreur signalée sur une entité ne s’applique plus).

Examinons un exemple qui réunit les points hello décrit. Examinons une application Service Fabric composée d’un service maître persistant avec état et de services subordonnés sans état déployés sur tous les nœuds (un type de service secondaire par type de tâche). maître de Hello dispose d’une file d’attente de traitement qui contient toobe commandes exécutée par les bases de données secondaires. bases de données secondaires Hello exécutent des demandes entrantes de hello et envoyer des signaux d’accusé de réception différé. Une condition qui peut être surveillée est la longueur de file d’attente de traitement principal hello hello. Si la longueur de file d’attente principale hello atteint un seuil, un avertissement est émis. Avertissement de Hello indique que bases de données secondaires hello ne peut pas traiter la charge de hello. Si la file d’attente hello atteint la longueur maximale de hello et commandes sont supprimées, une erreur est signalée, comme hello service ne peut pas récupérer. les rapports Hello peuvent être sur la propriété de hello **QueueStatus**. surveillance de Hello réside à l’intérieur de hello service, et il est régulièrement envoyée sur le réplica principal maître de hello. Hello toolive prend deux minutes, et il est envoyé régulièrement toutes les 30 secondes. Si hello principal tombe en panne, les rapports de hello est automatiquement nettoyée à partir du magasin. Si le réplica de service hello est activée, mais elle est bloquée ou avoir d’autres problèmes, hello rapport arrive à expiration dans le magasin de contrôle d’intégrité hello. Dans ce cas, les entités hello sont évaluée au niveau de l’erreur.

L’heure d’exécution de la tâche est une autre condition qui peut être surveillée. Hello maître distribue les tâches de bases de données secondaires toohello selon le type de tâche hello. En fonction de la conception de hello, maître de hello peut interroger secondaires hello pour l’état de la tâche. Il peut également attendre pour les bases de données secondaires toosend accusé de réception différé signaux lorsqu’elles sont effectuées. Dans les cas de deuxième hello, être vigilant toodetect les situations où les messages ou matrice de bases de données secondaires sont conservés. Une option est pour toosend maître de hello un toohello de demande ping secondaire, qui renvoie son état. Si aucun état n’est reçu, maître de hello considère comme un échec et replanifie la tâche hello. Ce comportement suppose que les tâches de hello sont idempotents.

condition de Hello analysé peut être traduite en tant qu’avertissement si la tâche hello n’est pas effectuée dans un certain temps (**t1**, par exemple 10 minutes). Si la tâche hello n’est pas terminée dans le temps (**t2**, par exemple 20 minutes), la condition de hello analysé peut être traduite en tant qu’erreur. Cette création de rapport peut se faire de plusieurs façons :

* réplica principal maître de Hello signale régulièrement sur lui-même. Vous pouvez avoir une propriété pour toutes les tâches en attente dans la file d’attente hello. Si au moins une tâche prend plus de temps, l’état d’hello sur la propriété de hello **PendingTasks** est un avertissement ou une erreur, comme il convient. Si aucune tâche en attente ou toutes les tâches a démarré l’exécution, l’état hello est OK. tâches de Hello sont persistantes. Si hello principal tombe en panne, principal de hello nouvellement promu peut continuer tooreport correctement.
* Un autre processus de surveillance (dans le cloud de hello ou externe) vérifie les tâches hello (à partir d’à l’extérieur, en fonction de résultat de la tâche hello souhaité) toosee si elles sont terminées. Si elles ne respectent pas les seuils de hello, un rapport est envoyé sur le service principal de hello. Un rapport est également envoyé sur chaque tâche incluant comme identificateur de la tâche hello, **PendingTask + taskId**. Des rapports ne doivent être envoyés que sur des états défectueux. Définissez tooa toolive de temps quelques minutes et marquez hello toobe de rapports supprimé à leur expiration tooensure nettoyage.
* Hello secondaire qui exécute une tâche signale quand il dure plus longtemps que prévu toorun il. Il signale sur l’instance du service hello sur la propriété de hello **PendingTasks**. met en évidence les rapports Hello instance du service hello qui présente des problèmes, mais il ne capture pas situation hello où perte, instance de hello. rapports de Hello sont nettoyés puis. Il a un rapport sur le service secondaire hello. Si hello secondaire termine la tâche hello, les instances secondaires hello efface rapport hello à partir du magasin de hello. rapport de Hello ne capture pas hello situation dans laquelle message d’accusé de réception hello est perdu tâche hello n’est pas terminé à partir du point de vue de la forme hello.

Toutefois hello reporting est effectué dans les cas de hello décrites ci-dessus, hello rapports sont capturées dans le contrôle d’intégrité de l’application lors de l’évaluation d’intégrité.

## <a name="report-periodically-vs-on-transition"></a>Rapport régulier ou sur transition
À l’aide de contrôle d’intégrité hello modèle de rapport, les agents de surveillance peuvent envoyer des rapports régulièrement ou sur les transitions. Hello recommandé pour la surveillance reporting consiste régulièrement, comme code de hello est bien tooerrors plus simple et moins sujet. agents de surveillance Hello doivent s’efforcent toobe aussi simple que possible tooavoid bogues qui déclenchent des rapports incorrects. Des rapport d’état *défectueux* incorrects ont une incidence sur les évaluations de l’intégrité et les scénarios basés sur l’intégrité, dont les mises à niveau. Incorrect *intègre* rapports masquer les problèmes dans un cluster de hello, qui n’est pas souhaité.

Création de rapports périodiques, surveillance de hello peut être implémenté avec un minuteur. Sur un rappel du minuteur, surveillance de hello peut vérifier l’état de hello et envoyer un rapport basé sur l’état actuel de hello. Il n’existe aucun toosee besoin de rapport a été envoyé précédemment ou effectuer des optimisations en termes de messagerie. client de contrôle d’intégrité Hello a toohelp logique dont les performances de traitement par lot. Alors que le client de contrôle d’intégrité hello reste actif, il effectue une nouvelle tentative en interne jusqu'à ce que les rapports hello sont acceptée par le magasin de contrôle d’intégrité hello ou de surveillance de hello génère un rapport plus récent avec hello même entité, property et source.

La génération de rapports sur les transitions nécessite une gestion prudente de l’état. surveillance de Hello surveille certaines conditions et signale uniquement lorsque les conditions hello changent. Hello envers de cette approche est que les rapports moins sont nécessaires. Hello inconvénient que la logique de surveillance de hello hello est complexe. surveillance de Hello doit mettre à jour les conditions de hello ou les rapports de hello, afin qu’ils puissent être inspecté toodetermine changements d’état. Lors du basculement, être vigilant avec les rapports ajouté, mais pas encore envoyés magasin de contrôle d’intégrité toohello. numéro de séquence Hello doit être croissante. Dans le cas contraire, les rapports hello sont rejetées comme obsolètes. Dans hello rares cas où une perte de données est générée, la synchronisation peut être nécessaire entre état hello du rapporteur de hello et état hello du magasin de contrôle d’intégrité hello.

La création de rapports sur les transitions est fondée pour les services de création de rapports sur eux-mêmes, via `Partition` ou `CodePackageActivationContext`. Lorsque hello objet local (réplica ou un package de service déployé / déployé l’application) est supprimé, tous ses rapports sont également supprimés. Le nettoyage automatique assouplit la nécessité de hello pour la synchronisation entre reporter et magasin de contrôle d’intégrité. Si le rapport de hello est pour la partition parente ou application parente, être vigilant sur le basculement tooavoid les rapports obsolètes dans le magasin de contrôle d’intégrité hello. Logique doit être ajoutée correcte de toomaintain hello et rapport de hello clair à partir du magasin si nécessaire, ne pas plus.

## <a name="implement-health-reporting"></a>Mise en œuvre de la création de rapports d’intégrité
Une fois que hello détails de l’entité et les rapports sont évidentes, rapports d’intégrité peut être envoyé par le biais des API de hello, PowerShell ou REST.

### <a name="api"></a>API
tooreport via hello API, vous devez toocreate un type d’entité d’intégrité rapport toohello spécifiques qu’ils souhaitent tooreport sur. Donnez un client de contrôle d’intégrité tooa hello rapports. Vous pouvez également créer une contrôle d’intégrité des informations et lui passer toocorrect méthodes de création de rapports sur `Partition` ou `CodePackageActivationContext` tooreport sur les entités en cours.

Hello suivant montre périodique de création de rapports à partir d’une surveillance au sein du cluster de hello. surveillance de Hello vérifie si une ressource externe sont accessibles à partir d’un nœud. ressource de Hello est requis par un manifeste de service au sein de l’application hello. Si les ressources hello ne sont pas disponible, hello autres services au sein de l’application hello continuent de fonctionner correctement. Par conséquent, les rapports hello sont envoyé sur l’entité de package de service hello déployé toutes les 30 secondes.

```csharp
private static Uri ApplicationName = new Uri("fabric:/WordCount");
private static string ServiceManifestName = "WordCount.Service";
private static string NodeName = FabricRuntime.GetNodeContext().NodeName;
private static Timer ReportTimer = new Timer(new TimerCallback(SendReport), null, 30 * 1000, 30 * 1000);
private static FabricClient Client = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });

public static void SendReport(object obj)
{
    // Test whether hello resource can be accessed from hello node
    HealthState healthState = this.TestConnectivityToExternalResource();

    // Send report on deployed service package, as hello connectivity is needed by hello specific service manifest
    // and can be different on different nodes
    var deployedServicePackageHealthReport = new DeployedServicePackageHealthReport(
        ApplicationName,
        ServiceManifestName,
        NodeName,
        new HealthInformation("ExternalSourceWatcher", "Connectivity", healthState));

    // TODO: handle exception. Code omitted for snippet brevity.
    // Possible exceptions: FabricException with error codes
    // FabricHealthStaleReport (non-retryable, hello report is already queued on hello health client),
    // FabricHealthMaxReportsReached (retryable; user should retry with exponential delay until hello report is accepted).
    Client.HealthManager.ReportHealth(deployedServicePackageHealthReport);
}
```

### <a name="powershell"></a>PowerShell
Envoyez les rapports d’intégrité avec **Send-ServiceFabric*EntityType*HealthReport**.

Hello suivant montre périodique de création de rapports sur les valeurs de l’UC sur un nœud. les rapports Hello doivent être envoyés à toutes les 30 secondes, et ils ont une heure toolive de deux minutes. S’ils expirent, rapporteur de hello présente des problèmes, nœud de hello est évaluée au niveau de l’erreur. Une fois hello UC au-dessus d’un seuil, les rapports hello a un état d’intégrité de l’avertissement. Lorsque hello du processeur reste supérieure à un seuil plus de temps de hello configuré, il est signalé comme une erreur. Dans le cas contraire, les reporter hello envoie un état d’intégrité de OK.

```powershell
PS C:\> Send-ServiceFabricNodeHealthReport -NodeName Node.1 -HealthState Warning -SourceId PowershellWatcher -HealthProperty CPU -Description "CPU is above 80% threshold" -TimeToLiveSec 120

PS C:\> Get-ServiceFabricNodeHealth -NodeName Node.1
NodeName              : Node.1
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='PowershellWatcher', Property='CPU', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 5
                        SentAt                : 4/21/2015 8:01:17 AM
                        ReceivedAt            : 4/21/2015 8:02:12 AM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/21/2015 8:02:12 AM

                        SourceId              : PowershellWatcher
                        Property              : CPU
                        HealthState           : Warning
                        SequenceNumber        : 130741236814913394
                        SentAt                : 4/21/2015 9:01:21 PM
                        ReceivedAt            : 4/21/2015 9:01:21 PM
                        TTL                   : 00:02:00
                        Description           : CPU is above 80% threshold
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/21/2015 9:01:21 PM
```

Hello exemple suivant signale un avertissement temporaire sur un réplica. Il obtient d’abord les ID de partition hello et puis hello ID de réplica pour le service hello qu'intéresse. Il envoie ensuite un rapport à partir de **PowershellWatcher** sur la propriété de hello **ResourceDependency**. rapport de Hello présente un intérêt pour que les deux minutes, et il est automatiquement supprimé à partir du magasin de hello.

```powershell
PS C:\> $partitionId = (Get-ServiceFabricPartition -ServiceName fabric:/WordCount/WordCount.Service).PartitionId

PS C:\> $replicaId = (Get-ServiceFabricReplica -PartitionId $partitionId | where {$_.ReplicaRole -eq "Primary"}).ReplicaId

PS C:\> Send-ServiceFabricReplicaHealthReport -PartitionId $partitionId -ReplicaId $replicaId -HealthState Warning -SourceId PowershellWatcher -HealthProperty ResourceDependency -Description "hello external resource that hello primary is using has been rebooted at 4/21/2015 9:01:21 PM. Expect processing delays for a few minutes." -TimeToLiveSec 120 -RemoveWhenExpired

PS C:\> Get-ServiceFabricReplicaHealth  -PartitionId $partitionId -ReplicaOrInstanceId $replicaId


PartitionId           : 8f82daff-eb68-4fd9-b631-7a37629e08c0
ReplicaId             : 130740415594605869
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='PowershellWatcher', Property='ResourceDependency', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130740768777734943
                        SentAt                : 4/21/2015 8:01:17 AM
                        ReceivedAt            : 4/21/2015 8:02:12 AM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/21/2015 8:02:12 AM

                        SourceId              : PowershellWatcher
                        Property              : ResourceDependency
                        HealthState           : Warning
                        SequenceNumber        : 130741243777723555
                        SentAt                : 4/21/2015 9:12:57 PM
                        ReceivedAt            : 4/21/2015 9:12:57 PM
                        TTL                   : 00:02:00
                        Description           : hello external resource that hello primary is using has been rebooted at 4/21/2015 9:01:21 PM. Expect processing delays for a few minutes.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : ->Warning = 4/21/2015 9:12:32 PM
```

### <a name="rest"></a>REST
Envoyer des rapports d’intégrité à l’aide de REST avec les demandes POST visitez toohello souhaité entité et dans la description du rapport d’intégrité hello corps hello. Par exemple, consultez Comment toosend REST [rapports d’intégrité de cluster](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-cluster) ou [rapports d’intégrité du service](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service). Toutes les entités sont prises en charge.

## <a name="next-steps"></a>Étapes suivantes
Selon les données de contrôle d’intégrité hello, aux développeurs de service et les administrateurs d’application/cluster peuvent considérer façons tooconsume hello d’informations. Par exemple, ils peuvent définir des alertes basées sur les problèmes graves toocatch d’état de contrôle d’intégrité avant de provoquer des pannes. Les administrateurs peuvent également définir des problèmes de réparation systèmes toofix automatiquement.

[Introduction tooService d’intégrité de l’infrastructure analyse](service-fabric-health-introduction.md)

[Affichage rapports d’intégrité de Service Fabric](service-fabric-view-entities-aggregated-health.md)

[Comment tooreport et vérification du service d’intégrité](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Utilisation des rapports d’intégrité système pour la résolution des problèmes](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[Surveiller et diagnostiquer les services localement](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Mise à niveau des applications Service Fabric](service-fabric-application-upgrade.md)

