---
title: "aaaWhat est Azure Scheduler ? | Microsoft Docs"
description: "Azure Scheduler vous permet de toodeclaratively décrivent toorun actions dans le cloud de hello. Ensuite, il planifie et exécute ces actions automatiquement."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 52aa6ae1-4c3d-43fb-81b0-6792c84bcfae
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 062e25ae473510264dc0038198c05e7ac1e86210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-scheduler"></a>Présentation d’Azure Scheduler
Azure Scheduler vous permet de toodeclaratively décrivent toorun actions dans le cloud de hello. Ensuite, il planifie et exécute ces actions automatiquement.  Planificateur de parvenir à l’aide de [hello portail Azure](scheduler-get-started-portal.md), code, [API REST](https://msdn.microsoft.com/library/mt629143.aspx), ou Azure PowerShell.

Le scheduler crée, gère et appelle le travail planifié.  Scheduler n’héberge pas de charge de travail et n’exécute pas de code. Il se contente d’ *appeler* du code qui est hébergé ailleurs, par exemple, dans Azure, localement ou auprès d’un autre fournisseur. Il effectue des appels via HTTP, HTTPS, une file d’attente de stockage, une file d’attente Service Bus ou une rubrique Service Bus.

Les planifications de planificateur [travaux](scheduler-concepts-terms.md), conserve un historique des résultats de l’exécution du travail qu’un peut examiner et de façon déterministe et fiable toobe de charges de travail de planifications exécuter. Les tâches Web Azure (partie de la fonctionnalité d’applications Web hello dans Azure App Service) et autres fonctionnalités de planification Azure utilisent le planificateur en arrière-plan de hello. Hello [API REST de Scheduler](https://msdn.microsoft.com/library/mt629143.aspx) permet de gérer la communication hello pour ces actions. Ainsi, Scheduler prend en charge les [planifications complexes et la périodicité avancée facilement](scheduler-advanced-complexity.md) .

Il existe plusieurs scénarios qui se prêtent à l’utilisation de toohello du planificateur. Par exemple :

* *Actions d’application périodiques* : collecte régulière de données à partir de Twitter dans un flux.
* *Maintenance quotidienne :* nettoyages quotidiens des journaux en exécutant des sauvegardes et autres tâches de maintenance. Par exemple, un administrateur peut choisir tooback base de données hello à 01:00. tous les jours hello prochains mois neuf.

Scheduler vous permet de toocreate mettre à jour, supprimer, afficher et gérer des travaux et [les collections de travaux](scheduler-concepts-terms.md) par programme, à l’aide de scripts et dans le portail de hello.

## <a name="see-also"></a>Voir aussi
 [Concepts, terminologie et hiérarchie d’entités d’Azure Scheduler](scheduler-concepts-terms.md)

 [Prise en main du planificateur Bonjour portail Azure](scheduler-get-started-portal.md)

 [Plans et facturation dans Azure Scheduler](scheduler-plans-billing.md)

 [Comment toobuild complexe planifie et périodicité avancée avec Azure Scheduler](scheduler-advanced-complexity.md)

 [Informations de référence sur l’API REST d’Azure Scheluler](https://msdn.microsoft.com/library/mt629143)

 [Informations de référence sur les applets de commande PowerShell d’Azure Scheluler](scheduler-powershell-reference.md)

 [Haute disponibilité et fiabilité d’Azure Scheluler](scheduler-high-availability-reliability.md)

 [Limites, valeurs par défaut et codes d’erreur d’Azure Scheluler](scheduler-limits-defaults-errors.md)

 [Authentification sortante d’Azure Scheluler](scheduler-outbound-authentication.md)

