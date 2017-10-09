---
title: "aaaScheduler haute disponibilité et fiabilité"
description: "Haute disponibilité et fiabilité de Scheduler"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 5ec78e60-a9b9-405a-91a8-f010f3872d50
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2016
ms.author: deli
ms.openlocfilehash: 5c9efb333eb42b393adc5deea657ca99206d425e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-high-availability-and-reliability"></a>Haute disponibilité et fiabilité de Scheduler
## <a name="azure-scheduler-high-availability"></a>Haute disponibilité d'Azure Scheduler
En tant que service central de la plateforme Microsoft Azure, Azure Scheduler est hautement disponible et propose le déploiement de service géo-redondant et la réplication de travail géo-régionale.

### <a name="geo-redundant-service-deployment"></a>Déploiement de service géo-redondant
Azure Scheduler est disponible via hello UI dans presque chaque région géographique dans Azure aujourd'hui. la liste des régions Azure Scheduler est disponible dans Hello est [répertoriés ici](https://azure.microsoft.com/regions/#services). Si un centre de données dans une région hébergée devient indisponible, les fonctionnalités de basculement hello d’Azure Scheduler sont telles que le service de hello est disponible à partir d’un autre centre de données.

### <a name="geo-regional-job-replication"></a>Réplication de travail géo-régionale
Non seulement est Bonjour Azure Scheduler frontal disponible pour les demandes de gestion, mais votre propre travail est également répliquées. Lorsqu’il existe une panne dans une région, Azure Scheduler bascule et garantit que le travail hello est exécuté à partir d’un autre centre de données dans la région géographique de hello associée.

Par exemple, si vous avez créé un travail dans le Centre-Sud des États-Unis, Azure Scheduler réplique automatiquement ce travail dans le Centre-Nord des États-Unis. Lorsqu’il y a un échec de l’Amérique du Sud, Azure Scheduler veille à ce que le travail hello est exécuté à partir de l’Amérique du Nord. 

![][1]

Par conséquent, Azure Scheduler garantit que vos données demeurent dans hello même région géographique élargie en cas d’échec d’Azure. Par conséquent, vous ne devez pas dupliquer votre travail simplement tooadd haute disponibilité, Azure Scheduler fournit automatiquement les fonctionnalités de haute disponibilité pour vos tâches.

## <a name="azure-scheduler-reliability"></a>Fiabilité d'Azure Scheduler
Azure Scheduler garantit sa propre haute disponibilité et adopte une approche différente travaux toouser créés. Par exemple, votre travail peut appeler un point de terminaison HTTP qui n'est pas disponible. Azure Scheduler tente néanmoins de mener tooexecute votre travail avec succès, en vous donnant toodeal d’autres options avec échec. Azure Scheduler effectue cette opération de deux manières :

### <a name="configurable-retry-policy-via-retrypolicy"></a>Stratégie de nouvelle tentative configurable avec « retryPolicy »
Azure Scheduler vous permet de tooconfigure une stratégie de nouvelle tentative. Par défaut, si une tâche échoue, le planificateur tente travail de hello quatre fois de plus, à des intervalles de 30 secondes. Vous pouvez reconfigurer cette nouvelle tentative stratégie toobe plus agressive (par exemple, dix fois, à des intervalles de 30 secondes) ou plus relâchée (par exemple, deux fois, à intervalles quotidiens.)

Pour illustrer quand cette fonction peut s'avérer utile, vous pouvez créer un travail qui s'exécute une fois par semaine et appelle un point de terminaison HTTP. Si le point de terminaison hello HTTP est arrêté pendant quelques heures lorsque votre tâche s’exécute, vouloir toowait semaine supplémentaire pour hello travail toorun à nouveau dans la mesure où même les stratégie de nouvelle tentative par défaut hello. Dans ce cas, vous pouvez reconfigurer tooretry de stratégie de nouvelle tentative standard hello toutes les trois heures (par exemple) au lieu de toutes les 30 secondes.

toolearn comment tooconfigure une stratégie de nouvelle tentative, consultez trop[retryPolicy](scheduler-concepts-terms.md#retrypolicy).

### <a name="alternate-endpoint-configurability-via-erroraction"></a>Capacité de configuration du point de terminaison alternatif avec « errorAction »
Si le point de terminaison cible hello pour votre travail Azure Scheduler reste inaccessible, Azure Scheduler bascule point de terminaison de gestion des erreurs secondaire toohello après avoir appliqué sa stratégie de nouvelle tentative. Si un point de terminaison alternatif de traitement des erreurs est configuré, Azure Scheduler l'appelle. Avec un autre point de terminaison, vos propres travaux est hautement disponibles en face de hello de défaillance.

Par exemple, dans le diagramme de hello ci-dessous, Azure Scheduler suit sa toohit de stratégie de nouvelle tentative un service web de New York. Une fois hello tentatives échouent, il vérifie s’il existe un autre. Il continue et démarre effectuant des demandes toohello alternent avec hello même stratégie de nouvelle tentative.

![][2]

Notez que la même stratégie de nouvelle tentative de hello s’applique action d’origine de tooboth hello et action d’erreur secondaire hello. Type d’action il également possible toohave hello autre erreur de l’action est différent du type d’action de l’action principale hello. Par exemple, tandis que l’action principale de hello peut appeler un point de terminaison HTTP, action d’erreur hello peut être à la place une file d’attente de stockage, une file d’attente du bus de service ou une action de rubrique service bus qui effectue la journalisation des erreurs.

toolearn comment tooconfigure un autre point de terminaison, consultez trop[errorAction](scheduler-concepts-terms.md#action-and-erroraction).

## <a name="see-also"></a>Voir aussi
 [Présentation d'Azure Scheduler](scheduler-intro.md)

 [Concepts, terminologie et hiérarchie d’entités d’Azure Scheduler](scheduler-concepts-terms.md)

 [Prise en main du planificateur Bonjour portail Azure](scheduler-get-started-portal.md)

 [Plans et facturation dans Azure Scheduler](scheduler-plans-billing.md)

 [Comment toobuild complexe planifie et périodicité avancée avec Azure Scheduler](scheduler-advanced-complexity.md)

 [Informations de référence sur l’API REST d’Azure Scheluler](https://msdn.microsoft.com/library/mt629143)

 [Informations de référence sur les applets de commande PowerShell d’Azure Scheluler](scheduler-powershell-reference.md)

 [Limites, valeurs par défaut et codes d’erreur d’Azure Scheluler](scheduler-limits-defaults-errors.md)

 [Authentification sortante d’Azure Scheluler](scheduler-outbound-authentication.md)

[1]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image1.png

[2]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image2.png
