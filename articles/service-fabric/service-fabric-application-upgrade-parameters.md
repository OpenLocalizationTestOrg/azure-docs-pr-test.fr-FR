---
title: "Mise à niveau d'une application : paramètres de mise à niveau | Microsoft Docs"
description: "Décrit les paramètres tooupgrading connexes une application Service Fabric, notamment d’intégrité vérifications tooperform et stratégies tooautomatically annulation hello mise à niveau."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a4170ac6-192e-44a8-b93d-7e39c92a347e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: abd0ba48c223be9aa0909c7a0100ba5986430db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-upgrade-parameters"></a>Paramètres de mise à niveau d'application
Cet article décrit hello divers paramètres qui s’appliquent au cours de hello mise à niveau d’une application Azure Service Fabric. les paramètres de Hello incluent le nom de hello et la version de l’application hello. Ils sont des boutons qui contrôlent les délais d’expiration hello et contrôles d’intégrité qui sont appliqués au cours de la mise à niveau hello et spécifient les stratégies hello qui doivent être appliquées en cas d’échec d’une mise à niveau.

<br>

| Paramètre | Description |
| --- | --- |
| ApplicationName |Nom de l’application hello qui est en cours de mise à niveau. Exemples : fabric:/VisualObjects, fabric:/ClusterMonitor |
| TargetApplicationTypeVersion |version de Hello du type d’application hello hello cibles de mise à niveau. |
| FailureAction |action de Hello effectuée par l’infrastructure de Service en cas d’échec de la mise à niveau hello. application Hello peut être restaurée version de mise à jour préalable toohello (rollback), ou mise à niveau hello est peut-être arrêté au domaine de mise à niveau actuel hello. Dans ce dernier cas de hello, mode de mise à niveau de hello est également modifié tooManual. Les valeurs autorisées sont Rollback et Manual. |
| HealthCheckWaitDurationSec |Hello toowait de temps (en secondes) après la mise à niveau hello est terminée sur le domaine de mise à niveau hello avant que le Service Fabric évalue l’intégrité hello application hello. Cette durée peut également être considérée comme temps hello qu'une application doit être en cours d’exécution avant qu’il peut être considéré comme sain. Si le contrôle d’intégrité de hello réussit, le processus de mise à niveau de hello continue toohello domaine de mise à niveau suivant.  En cas de contrôle d’intégrité de hello, Service Fabric attend un intervalle (hello UpgradeHealthCheckInterval) avant de réessayer d’intégrité hello jusqu'à hello que healthcheckretrytimeout est atteinte. valeur par défaut Hello et la valeur recommandée est de 0 seconde. |
| HealthCheckRetryTimeoutSec |Durée Hello (en secondes) qui continue de l’infrastructure de Service tooperform l’évaluation d’intégrité avant de déclarer la mise à niveau hello comme ayant échoué. valeur par défaut Hello est de 600 secondes. Cette durée commence quand HealthCheckWaitDuration est atteint. Dans cette HealthCheckRetryTimeout, Service Fabric peut effectuer plusieurs contrôles d’intégrité d’application hello. valeur par défaut de Hello est de 10 minutes et doit être personnalisé de manière appropriée pour votre application. |
| HealthCheckStableDurationSec |durée (en secondes) de Hello tooverify qu’application hello est stable avant de domaine de mise à niveau suivant toohello mobile ou de fin de bienvenue mise à niveau. Cette durée d’attente est utilisé tooprevent pas détecté des modifications de l’intégrité de le fois que le contrôle d’intégrité de hello est effectué. valeur par défaut de Hello est de 120 secondes et doit être personnalisé de manière appropriée pour votre application. |
| UpgradeDomainTimeoutSec |Durée maximale (en secondes) pour mettre à niveau un seul domaine de mise à niveau. Si ce délai est atteint, mise à niveau hello s’arrête et se poursuit en fonction de paramètre hello pour UpgradeFailureAction. valeur par défaut de Hello n’est jamais (infini) et doit être personnalisé de manière appropriée pour votre application. |
| UpgradeTimeout |Un délai d’attente (en secondes) qui s’appliquent pour la mise à niveau entière de hello. Si ce délai est atteint, hello mise à niveau s’arrête et UpgradeFailureAction est déclenchée. valeur par défaut de Hello n’est jamais (infini) et doit être personnalisé de manière appropriée pour votre application. |
| UpgradeHealthCheckInterval |fréquence de Hello hello l’état d’intégrité est vérifiée. Ce paramètre est spécifié dans la section ClusterManager Hello de hello *cluster* *manifeste*et n’est pas spécifié dans le cadre de l’applet de commande hello mise à niveau. Hello par défaut est 60 secondes. |

<br>

## <a name="service-health-evaluation-during-application-upgrade"></a>Évaluation de l'intégrité du service au cours de la mise à niveau de l'application
<br>
les critères d’évaluation d’intégrité Hello sont facultatifs. Si les critères d’évaluation d’intégrité hello ne sont pas spécifiées au démarrage d’une mise à niveau, Service Fabric utilise des stratégies de contrôle d’intégrité d’application hello spécifiés dans hello ApplicationManifest.xml de l’instance de l’application hello.

<br>

| Paramètre | Description |
| --- | --- |
| ConsiderWarningAsError |La valeur par défaut est False. Traiter les événements de contrôle d’intégrité d’avertissement hello pour une application hello comme des erreurs lors de l’évaluation d’intégrité hello application hello pendant la mise à niveau. Par défaut, Service Fabric n’évalue pas les échecs de toobe avertissement d’intégrité événements (erreurs), mise à niveau hello peut continuer même si les événements d’avertissement. |
| MaxPercentUnhealthyDeployedApplications |La valeur par défaut et recommandée est 0. Spécifiez le nombre maximal de hello des applications déployées (voir hello [section intégrité](service-fabric-health-introduction.md)) qui peut être non intègres avant de l’application hello est considéré comme non intègre et échoue hello mise à niveau. Ce paramètre définit l’intégrité des applications hello sur le nœud de hello et vous aide à détecter les problèmes de mise à jour. En règle générale, les réplicas hello de l’application hello obtient toohello d’équilibrage de la charge autre nœud, ce qui permet de hello application tooappear intègre, ce qui permet de tooproceed de mise à niveau hello. En spécifiant un contrôle d’intégrité MaxPercentUnhealthyDeployedApplications strict, Service Fabric peut détecter un problème avec le package d’application hello rapidement et aider à produire un échec rapide de mise à niveau. |
| MaxPercentUnhealthyServices |La valeur par défaut et recommandée est 0. Spécifiez le nombre maximal de hello de services dans l’instance de l’application hello qui peut être non intègre avant de l’application hello est considéré comme non intègre et Échec de mise à niveau hello. |
| MaxPercentUnhealthyPartitionsPerService |La valeur par défaut et recommandée est 0. Spécifiez le nombre maximal de hello de partitions dans un service qui peut être non intègre avant que le service de hello est considéré comme non intègre. |
| MaxPercentUnhealthyReplicasPerPartition |La valeur par défaut et recommandée est 0. Spécifiez le nombre maximal de hello de réplicas dans la partition peut être non intègre avant de la partition de hello est considéré comme non intègre. |
| UpgradeReplicaSetCheckTimeout |**Service sans état**--tente de tooensure que des instances supplémentaires du service de hello sont disponibles dans un seul domaine de mise à niveau, l’infrastructure de Service. Si le nombre d’instances cible hello est supérieur à un, l’infrastructure de Service attend que plusieurs toobe instance disponible, valeur de délai d’attente maximal tooa. Ce délai d’expiration est spécifiée à l’aide des propriétés de UpgradeReplicaSetCheckTimeout hello. Si l’expiration du délai hello, Service Fabric se poursuit avec la mise à niveau de hello, quel que soit le nombre de hello d’instances de service. Si le nombre d’instances cible hello est un, Service Fabric n’attend pas et passe immédiatement avec mise à niveau hello. **Un service avec état**--dans un seul domaine de mise à niveau, Service Fabric tente tooensure qui hello réplica jeu possède un quorum. L’infrastructure de service attend un toobe de quorum disponible, valeur de délai d’attente maximal tooa (spécifié par la propriété de UpgradeReplicaSetCheckTimeout hello). Si l’expiration du délai hello, Service Fabric se poursuit avec la mise à niveau de hello, quel que soit le quorum. Ce paramètre est défini sur « never » (infini) pour une restauration par progression et sur 900 secondes pour une restauration. |
| ForceRestart |Si vous mettez à jour une configuration ou un package de données sans mettre à jour le code de service hello, service de hello est redémarré uniquement si hello ForceRestart propriété a la valeur tootrue. Lors de la mise à jour hello est terminée, le Service Fabric notifie service de hello qu’un nouveau package de configuration ou d’un package de données est disponible. service de Hello est responsable de l’application des modifications de hello. Si nécessaire, le service de hello peut redémarrer lui-même. |

<br>
<br>
critères de MaxPercentUnhealthyServices, MaxPercentUnhealthyPartitionsPerService et MaxPercentUnhealthyReplicasPerPartition de Hello peuvent être spécifiés par le type de service pour une instance d’application. Définition de ces paramètres par service autorise une application toocontain différents services types avec des stratégies différentes d’évaluation. Par exemple, pour une instance d’application donnée, un type de service de passerelle sans état et un type de service de moteur avec état peuvent avoir des valeurs MaxPercentUnhealthyPartitionsPerService différentes.

## <a name="next-steps"></a>Étapes suivantes
[mise à niveau de votre application à l’aide de Visual Studio](service-fabric-application-upgrade-tutorial.md) vous guide à travers une mise à niveau de l’application à l’aide de Visual Studio.

[mise à niveau de votre application à l’aide de PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) vous guide à travers une mise à niveau de l’application à l’aide de PowerShell.

[Mise à niveau de votre application en utilisant l’interface CLI Service Fabric sur Linux](service-fabric-application-lifecycle-sfctl.md#upgrade-application) vous guide tout au long des étapes de mise à niveau de l’application avec l’interface CLI Service Fabric.

[Mise à niveau de votre application avec le plug-in Eclipse Service Fabric](service-fabric-get-started-eclipse.md#upgrade-your-service-fabric-java-application)

Rendre les mises à niveau de votre application compatible par learning comment toouse [sérialisation des données](service-fabric-application-upgrade-data-serialization.md).

Découvrez comment toouse des fonctionnalités avancées lors de la mise à niveau de votre application en vous reportant trop[rubriques avancées](service-fabric-application-upgrade-advanced.md).

Résoudre les problèmes courants dans les mises à niveau de l’application en faisant référence à des étapes de toohello de [résolution des problèmes de mises à niveau Application](service-fabric-application-upgrade-troubleshooting.md).
