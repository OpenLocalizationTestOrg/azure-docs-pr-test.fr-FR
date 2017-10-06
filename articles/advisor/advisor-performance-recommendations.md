---
title: "recommandations de l’Assistant Performance aaaAzure | Documents Microsoft"
description: "Utiliser l’Assistant toooptimize hello les performances de vos déploiements Azure."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: eb3d928664717f6f322132ac740f42015f56b76e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-performance-recommendations"></a>Recommandations Azure Advisor en matière de performances

Recommandations de performances l’Assistant Azure aider à améliorer la vitesse de hello et la réactivité de vos applications critiques. Vous pouvez obtenir des recommandations relatives aux performances du conseiller sur hello **performances** onglet du tableau de bord hello Advisor.

![Onglet Performances du conseiller](./media/advisor-performance-recommendations/advisor-performance-tab.png)

## <a name="improve-database-performance-with-sql-db-advisor"></a>Améliorer les performances de base de données avec SQL DB Advisor

Le conseiller vous offre une vue cohérente et consolidée des recommandations pour toutes vos ressources Azure. Il s’intègre avec l’Assistant de base de données SQL toobring vous recommandations pour améliorer les performances de hello de votre base de données SQL Azure. Assistant de base de données SQL évalue les performances hello vos bases de données SQL Azure en analysant votre historique d’utilisation. Il propose de recommandations les mieux adaptées à la charge de travail classique hello de base de données en cours d’exécution. 

> [!NOTE]
> recommandations de tooget, une base de données doit avoir une semaine de l’utilisation, et au sein de la semaine doit être une activité cohérente. SQL Database Advisor peut plus facilement optimiser les modèles de requête cohérents que les pics d’activité aléatoires.

Pour plus d’informations sur SQL Database Advisor, consultez la page [SQL Database Advisor](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).

![Recommandations SQL Database](./media/advisor-performance-recommendations/advisor-performance-sql.png)

## <a name="improve-redis-cache-performance-and-reliability"></a>Améliorer la fiabilité et les performances du Cache Redis

Advisor identifie les instances de Cache Redis où les performances peuvent être défavorablement affectées par une utilisation intensive de la mémoire, la charge du serveur, la bande passante réseau ou un grand nombre de connexions clientes. Advisor fournit également des meilleures pratiques toohelp recommandations vous éviterez des problèmes potentiels. Pour plus d’informations concernant les recommandations de Cache Redis, consultez [Redis Cache Advisor](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).


## <a name="improve-app-service-performance-and-reliability"></a>Améliorer la fiabilité et les performances d’App Service

Le conseiller Azure intègre des recommandations quant aux meilleures pratiques pour améliorer votre expérience App Services et vous faire découvrir des fonctionnalités appropriées de la plateforme. Exemples de recommandations App Services :
* Détection des instances où les ressources de mémoire ou de processeur sont épuisées par des exécutions d’application avec options d’atténuation.
* Détection des instances où la colocalisation de ressources telles que les applications web et les bases de données peut améliorer les performances et réduire les coûts. 

Pour plus d’informations sur les recommandations App Services, consultez [Meilleures pratiques pour Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).
![Recommandations App Services](./media/advisor-performance-recommendations/advisor-performance-app-service.png)

## <a name="how-tooaccess-performance-recommendations-in-advisor"></a>Comment tooaccess recommandations relatives aux performances dans l’Assistant

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).

2. Dans le volet gauche de hello, cliquez sur **davantage de services**.

3. Bonjour service sous le volet de menu, **analyse et gestion**, cliquez sur **Azure Advisor**.  
 tableau de bord Hello Advisor s’affiche.

4. Tableau de bord du conseiller hello, cliquez sur hello **performances** onglet.

5. Sélectionnez l’abonnement hello pour lequel vous souhaitez que les recommandations tooreceive, puis cliquez sur **obtenir des recommandations**.

> [!NOTE]
> tooaccess recommandations de l’Assistant, vous devez d’abord *enregistrer votre abonnement* avec l’Assistant. Un abonnement est enregistré quand un *abonnement propriétaire* lance hello hello de tableau de bord et clique sur Advisor **obtenir des recommandations** bouton. Cette opération ne doit être *exécutée qu’une seule fois*. Une fois l’abonnement de hello est enregistré, vous pouvez accéder à des recommandations de l’Assistant en tant que *propriétaire*, *collaborateur*, ou *lecteur* pour un abonnement, un groupe de ressources, ou un ressource spécifique.

## <a name="next-steps"></a>Étapes suivantes

toolearn en savoir plus sur les recommandations de l’Assistant, consultez :

* [Introduction tooAdvisor](advisor-overview.md)
* [Prise en main du conseiller](advisor-get-started.md)
* [Recommandations du conseiller en matière de coûts](advisor-performance-recommendations.md)
* [Recommandations du conseiller en matière de haute disponibilité](advisor-high-availability-recommendations.md)
* [Recommandations du conseiller en matière de sécurité](advisor-security-recommendations.md)

