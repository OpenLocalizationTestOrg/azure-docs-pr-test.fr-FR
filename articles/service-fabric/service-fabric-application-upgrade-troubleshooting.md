---
title: "mises à niveau des applications aaaTroubleshooting | Documents Microsoft"
description: "Cet article aborde certains problèmes courants autour de la mise à niveau une application de Service Fabric et comment tooresolve les."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 19ad152e-ec50-4327-9f19-065c875c003c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 0f56fa61db9b4e32824623f162dc1bfe7fda0f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-application-upgrades"></a>Résoudre les problèmes de mise à niveau d'application
Cet article décrit certains des problèmes courants de hello autour de la mise à niveau une application Azure Service Fabric et comment tooresolve les.

## <a name="troubleshoot-a-failed-application-upgrade"></a>Résoudre les problèmes liés à l'échec de la mise à niveau d'une application
Lorsqu’une mise à niveau échoue, sortie hello Hello **Get-ServiceFabricApplicationUpgrade** commande contient des informations supplémentaires pour le débogage d’échec de hello.  Hello liste suivante indique comment les informations supplémentaires de hello peuvent être utilisées :

1. Identifier le type d’échec hello.
2. Identifiez la raison de l’échec hello.
3. Isoler le ou les composants défectueux en vue d’un examen approfondi.

Ces informations sont disponibles lorsque le Service Fabric détecte l’échec de hello, indépendamment de si hello **FailureAction** tooroll DOS ou suspendre la mise à niveau hello.

### <a name="identify-hello-failure-type"></a>Identifier le type d’échec hello
Dans la sortie de hello de **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identifie hello horodateur (UTC) à laquelle un échec de mise à niveau a été détecté par l’infrastructure de Service et  **FailureAction** a été déclenchée. **Raison de l’échec** identifie l’un de trois causes principales de l’échec de hello :

1. UpgradeDomainTimeout - indique qu’un domaine de mise à niveau particulier a pris trop de temps toocomplete et **UpgradeDomainTimeout** a expiré.
2. OverallUpgradeTimeout - indique que hello globale de mise à niveau a duré trop long toocomplete et **UpgradeTimeout** a expiré.
3. Vérification de l’intégrité - indique qu’après la mise à niveau un domaine de mise à jour, application hello est restée défectueuse selon toohello spécifié des stratégies d’intégrité et **HealthCheckRetryTimeout** a expiré.

Ces entrées apparaissent seulement dans la sortie de hello lors de la mise à niveau hello échoue et démarre l’annulation. Informations complémentaires sont affichées en fonction de type hello de défaillance de hello.

### <a name="investigate-upgrade-timeouts"></a>Examiner les dépassements de délai d'attente de mise à niveau
Les échecs de délai d'attente de mise à niveau sont généralement dus à des problèmes de disponibilité de service. sortie Hello ci-dessous est typique de mises à niveau si les réplicas de service ou les instances ne toostart dans la nouvelle version de code hello. Hello **UpgradeDomainProgressAtFailure** champ capture un instantané de tout travail de mise à niveau en attente au moment de hello de défaillance.

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                : fabric:/DemoApp
ApplicationTypeName            : DemoAppType
TargetApplicationTypeVersion   : v2
ApplicationParameters          : {}
StartTimestampUtc              : 4/14/2015 9:26:38 PM
FailureTimestampUtc            : 4/14/2015 9:27:05 PM
FailureReason                  : UpgradeDomainTimeout
UpgradeDomainProgressAtFailure : MYUD1

                                 NodeName            : Node4
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 744c8d9f-1d26-417e-a60e-cd48f5c098f0

                                 NodeName            : Node1
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 4b43f4d8-b26b-424e-9307-7a7a62e79750
UpgradeState                   : RollingBackCompleted
UpgradeDuration                : 00:00:46
CurrentUpgradeDomainDuration   : 00:00:00
NextUpgradeDomain              :
UpgradeDomainsStatus           : { "MYUD1" = "Completed";
                                 "MYUD2" = "Completed";
                                 "MYUD3" = "Completed" }
UpgradeKind                    : Rolling
RollingUpgradeMode             : UnmonitoredAuto
ForceRestart                   : False
UpgradeReplicaSetCheckTimeout  : 00:00:00
```

Dans cet exemple, mise à niveau hello échec au niveau du domaine de mise à niveau *MYUD1* et deux partitions (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* et *4b43f4d8-b26b-424e-9307-7a7a62e79750*) ont été bloqués. les partitions Hello ont été bloquées car hello runtime a été impossible de tooplace les réplicas principaux (*WaitForPrimaryPlacement*) sur les nœuds cibles *Node1* et *Node4*.

Hello **Get-ServiceFabricNode** commande peut être utilisé tooverify que ces deux nœuds sont dans le domaine de mise à niveau *MYUD1*. Hello *UpgradePhase* indique que *PostUpgradeSafetyCheck*, ce qui signifie que ces contrôles de sécurité sont produisent une fois tous les nœuds dans le domaine de mise à niveau hello ont terminé la mise à niveau. Toutes ces informations pointant tooa le problème potentiel avec hello nouvelle version du code de l’application hello. les problèmes les plus courants Hello des erreurs service hello open ou les chemins de code de promotion tooprimary.

Un *UpgradePhase* de *PreUpgradeSafetyCheck* signifie problèmes de domaine de mise à niveau hello avant qu’il a été effectuée. Dans ce cas, les problèmes les plus courants Hello sont erreurs service hello fermer ou de rétrogradation à partir des chemins de code principal.

Hello actuel **UpgradeState** est *RollingBackCompleted*, de sorte que la mise à niveau d’origine de hello doit avoir été effectuée avec une restauration **FailureAction**, qui automatiquement restaurée de la mise à niveau hello en cas d’échec. Si une mise à niveau d’origine de hello a été effectuée d’une opération manuelle **FailureAction**, puis de la mise à niveau hello serait à la place dans un état suspendu de tooallow dynamique de débogage de l’application hello.

### <a name="investigate-health-check-failures"></a>Examiner les échecs des contrôles d'intégrité
Des échecs de contrôle d’intégrité peuvent être déclenchés par divers problèmes qui peuvent se produire après la mise à niveau de tous les nœuds dans un domaine de mise à niveau et la réussite de tous les contrôles de sécurité. sortie Hello ci-dessous est typique d’un échec de mise à niveau en raison des contrôles d’intégrité de toofailed. Hello **UnhealthyEvaluations** champ capture un instantané des contrôles d’intégrité qui a échoué lors de mise à niveau hello selon toohello spécifié hello [stratégie d’intégrité](service-fabric-health-introduction.md).

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                         : fabric:/DemoApp
ApplicationTypeName                     : DemoAppType
TargetApplicationTypeVersion            : v4
ApplicationParameters                   : {}
StartTimestampUtc                       : 4/24/2015 2:42:31 AM
UpgradeState                            : RollingForwardPending
UpgradeDuration                         : 00:00:27
CurrentUpgradeDomainDuration            : 00:00:27
NextUpgradeDomain                       : MYUD2
UpgradeDomainsStatus                    : { "MYUD1" = "Completed";
                                          "MYUD2" = "Pending";
                                          "MYUD3" = "Pending" }
UnhealthyEvaluations                    :
                                          Unhealthy services: 50% (2/4), ServiceType='PersistedServiceType', MaxPercentUnhealthyServices=0%.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc3', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='3a9911f6-a2e5-452d-89a8-09271e7e49a8', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc2', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='744c8d9f-1d26-417e-a60e-cd48f5c098f0', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

UpgradeKind                             : Rolling
RollingUpgradeMode                      : Monitored
FailureAction                           : Manual
ForceRestart                            : False
UpgradeReplicaSetCheckTimeout           : 49710.06:28:15
HealthCheckWaitDuration                 : 00:00:00
HealthCheckStableDuration               : 00:00:10
HealthCheckRetryTimeout                 : 00:00:10
UpgradeDomainTimeout                    : 10675199.02:48:05.4775807
UpgradeTimeout                          : 10675199.02:48:05.4775807
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :
```

Enquête sur les échecs de vérification d’intégrité exige en premier lieu une présentation du modèle de contrôle d’intégrité de l’infrastructure de Service hello. Mais même sans ces approfondies, nous pouvons voir que les deux services ne sont pas intègres : *fabric : / DemoApp/Svc3* et *fabric : / DemoApp/Svc2*, ainsi que les rapports d’intégrité erreur hello (« InjectedFault « Dans ce cas). Dans cet exemple, deux des quatre services sont défectueux, ce qui est sous la cible par défaut de hello de 0 % défectueux (*MaxPercentUnhealthyServices*).

Hello mise à niveau a été suspendu lors de l’échec en spécifiant un **FailureAction** de manuelle lorsque démarrage hello mise à niveau. Ce mode permet tooinvestigate hello dynamique du système en état de hello a échoué avant toute autre action.

### <a name="recover-from-a-suspended-upgrade"></a>Récupérer à partir d'une mise à niveau suspendue
Avec une restauration **FailureAction**, il n’existe aucune récupération n’est nécessaire car la mise à niveau hello restaure automatiquement sur l’échec. Si une opération **FailureAction**manuelle est définie, plusieurs options de récupération existent :

1.  Déclencher une restauration
2. Suivez les étapes reste hello de mise à niveau hello manuellement
3. Hello de CV analysée mise à niveau

Hello **ServiceFabricApplicationRollback de début** à n’importe quel toostart temps annulation application hello, vous pouvez utiliser la commande. Une fois la commande hello est retournée avec succès, une requête rollback hello a été inscrit dans le système de hello et démarre peu de temps après.

Hello **Resume-ServiceFabricApplicationUpgrade** commande peut être utilisée tooproceed via reste hello Hello mise à niveau manuellement, un seul domaine de mise à niveau à la fois. Dans ce mode, les vérifications de sécurité uniquement effectuées par ce hello. Aucun contrôle d’intégrité supplémentaire n’est effectué. Cette commande peut être utilisée uniquement lorsque hello *UpgradeState* montre *RollingForwardPending*, ce qui signifie que ce domaine de mise à niveau en cours hello a terminé la mise à niveau, mais hello ensuite une n’a pas démarré (en attente).

Hello **mise à jour-ServiceFabricApplicationUpgrade** commande peut être mise à niveau de hello analysé tooresume utilisés avec les vérifications de sécurité et de santé en cours.

```
PS D:\temp> Update-ServiceFabricApplicationUpgrade fabric:/DemoApp -UpgradeMode Monitored

UpgradeMode                             : Monitored
ForceRestart                            :
UpgradeReplicaSetCheckTimeout           :
FailureAction                           :
HealthCheckWaitDuration                 :
HealthCheckStableDuration               :
HealthCheckRetryTimeout                 :
UpgradeTimeout                          :
UpgradeDomainTimeout                    :
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :

PS D:\temp>
```

mise à niveau de Hello continue à partir de domaine de mise à niveau hello dans laquelle il a été interrompu en dernier et hello utilisez même mettre à niveau les paramètres et stratégies d’intégrité en tant qu’avant. Si nécessaire, un des paramètres de mise à niveau hello et stratégies d’intégrité illustrés hello précédant la sortie peut être modifié dans hello même commande lors de la mise à niveau hello reprend. Dans cet exemple, la mise à niveau hello a repris en mode surveillés, avec des paramètres de hello et de stratégies d’intégrité hello inchangées.

## <a name="further-troubleshooting"></a>Suite de la résolution des problèmes
### <a name="service-fabric-is-not-following-hello-specified-health-policies"></a>L’infrastructure de service n’est pas les hello spécifié stratégies d’intégrité
Cause possible 1 :

L’infrastructure de service se traduit par des pourcentages tous les chiffres réels d’entités (par exemple, les réplicas, partitions et les services) pour l’évaluation d’intégrité et arrondit toujours des entités de toowhole. Par exemple, si hello maximale *MaxPercentUnhealthyReplicasPerPartition* est 21 % et il existe cinq réplicas, puis le Service Fabric permet des réplicas de fonctionnement anormal tootwo (autrement dit,`Math.Ceiling (5*0.21)`). Par conséquent, les stratégies de contrôle d’intégrité doivent être définies pour tenir compte de cela.

Cause possible 2 :

Les stratégies d'intégrité sont spécifiées en pourcentages du nombre total de services et non en instances de service spécifiques. Par exemple, avant une mise à niveau, si une application possède quatre instances A, B, C et D, de service où service D n’est pas intègre, mais avec application de toohello faible impact. Nous souhaitons hello tooignore connue de service non intègre D lors de paramètre de mise à niveau et définissez hello *MaxPercentUnhealthyServices* toobe 25 %, en supposant seulement A, B et C doivent toobe sain.

Toutefois, au cours de la mise à niveau de hello, D peut-être devenir intègre tandis que C devient non intègre. mise à niveau Hello réussit toujours, car seuls 25 % de services de hello ne sont pas intègres. Toutefois, cela peut entraîner des erreurs imprévues échéance tooC en cours défectueux de façon inattendue au lieu de D. Dans ce cas, D doit être modélisée comme un type de service différent de A, B et C. Étant donné que les stratégies d’intégrité sont spécifiés par le type de service, les seuils de pourcentage anormal différent peuvent être appliqué toodifferent services. 

### <a name="i-did-not-specify-a-health-policy-for-application-upgrade-but-hello-upgrade-still-fails-for-some-time-outs-that-i-never-specified"></a>Je ne spécifiait pas une stratégie de contrôle d’intégrité pour la mise à niveau de l’application, mais la mise à niveau hello échoue pour des délais d’expiration spécifiée jamais
Lorsque les stratégies d’intégrité ne sont pas fournis de demande de mise à niveau toohello, elles sont tirées de hello *ApplicationManifest.xml* de la version actuelle de l’application hello. Par exemple, si vous mettez à niveau X de l’Application à partir de la version 1.0 tooversion 2.0, les stratégies de contrôle d’intégrité d’application spécifiés pour la version 1.0 sont utilisés. Si une autre stratégie d’intégrité doit être utilisée pour la mise à niveau hello, stratégie de hello doit toobe spécifié dans le cadre de l’appel d’API hello application mise à niveau. Hello stratégies spécifiées dans le cadre de l’appel d’API de hello s’appliquent uniquement au cours de la mise à niveau hello. Une fois la mise à niveau hello est terminée, les stratégies de hello spécifiées Bonjour *ApplicationManifest.xml* sont utilisés.

### <a name="incorrect-time-outs-are-specified"></a>Délais d’attente incorrects spécifiés
Vous vous demandez peut-être ce qui se passe lorsque les délais d’expiration sont définis de façon incohérente. Par exemple, vous pouvez avoir un *UpgradeTimeout* qui est inférieur à hello *UpgradeDomainTimeout*. les réponses Hello sont qu’une erreur est retournée. Les erreurs sont retournées si hello *UpgradeDomainTimeout* est inférieure à la somme de hello de *HealthCheckWaitDuration* et *HealthCheckRetryTimeout*, ou si  *UpgradeDomainTimeout* est inférieure à la somme de hello de *HealthCheckWaitDuration* et *HealthCheckStableDuration*.

### <a name="my-upgrades-are-taking-too-long"></a>Mes mises à niveau prennent trop de temps
temps de Hello pour une mise à niveau toocomplete dépend de vérifications d’intégrité de hello et délais d’expiration spécifiés. Contrôles d’intégrité et les délais d’expiration dépendent de la durée toocopy, déploiement et stabilisent application hello. Se montrer trop sévère avec les délais d’attente peut induire plus d’échecs de mises à niveau ; nous vous recommandons donc de démarrer prudemment avec des délais d’attente plus longs.

Voici un rappel rapide sur l’interagissent des délais d’expiration hello tentatives de mise à niveau hello :

Les mises à niveau pour un domaine de mise à niveau ne peuvent pas prendre moins de temps que *HealthCheckWaitDuration* + *HealthCheckStableDuration*.

Un échec de mise à niveau ne peut pas se produire avant *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.

temps de mise à niveau pour un domaine de mise à niveau Hello est limitée par *UpgradeDomainTimeout*.  Si *HealthCheckRetryTimeout* et *HealthCheckStableDuration* sont différente de zéro et la santé de l’application hello hello conserve va-et-vient, puis mise à niveau hello finalement arrive à expiration sur  *UpgradeDomainTimeout*. *UpgradeDomainTimeout* démarre une fois le comptage vers le bas hello mise à niveau pour le domaine de mise à niveau actuel hello commence.

## <a name="next-steps"></a>Étapes suivantes
[mise à niveau de votre application à l’aide de Visual Studio](service-fabric-application-upgrade-tutorial.md) vous guide à travers une mise à niveau de l’application à l’aide de Visual Studio.

[mise à niveau de votre application à l’aide de PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) vous guide à travers une mise à niveau de l’application à l’aide de PowerShell.

Contrôlez les mises à niveau de votre application à l'aide des [Paramètres de mise à niveau](service-fabric-application-upgrade-parameters.md).

Rendre les mises à niveau de votre application compatible par learning comment toouse [sérialisation des données](service-fabric-application-upgrade-data-serialization.md).

Découvrez comment toouse des fonctionnalités avancées lors de la mise à niveau de votre application en vous reportant trop[rubriques avancées](service-fabric-application-upgrade-advanced.md).
