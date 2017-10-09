---
title: "aaaView activités Windows Azure se connecte avec Analytique de journal | Documents Microsoft"
description: "Vous pouvez utiliser hello journaux d’activité Azure solution tooanalyze et journal des activités Windows Azure hello recherche dans tous vos abonnements Azure."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: dbac4c73-0058-4191-a906-e59aca8e2ee0
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.openlocfilehash: 171d0d604d03a5714a9599cc0b448fc5f6471f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="view-azure-activity-logs"></a>Consulter des journaux d’activité Azure

![Symbole des journaux d’activité Azure](./media/log-analytics-activity/activity-log-analytics.png)

Hello solution d’Analytique de journal d’activité vous permet d’analyser et de recherche hello [journal des activités Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) dans tous vos abonnements Azure. Hello journal des activités Azure est un journal qui offre un aperçu hello les opérations effectuées sur les ressources dans vos abonnements. Hello journal d’activité était précédemment appelé *les journaux d’Audit* ou *journaux opérationnels* dans la mesure où il signale les événements pour vos abonnements.

À l’aide de hello journal d’activité, vous pouvez déterminer hello *que*, *qui*, et *lorsque* pour les opérations d’écriture (PUT, POST, DELETE) effectuées pour les ressources hello dans votre abonnement. Vous pouvez également comprendre état hello d’opérations de hello et d’autres propriétés pertinentes. Hello journal d’activité n’inclut pas les opérations de (GET) en lecture ou de ressources qui utilisent le modèle de déploiement classique hello.

Lorsque vous vous connectez votre tooLog de journaux des activités Windows Azure Analytique, vous pouvez :

- Analyser les journaux d’activité hello avec des vues prédéfinies
- Analyser et rechercher des journaux d’activité parmi plusieurs abonnements Azure
- Conserver les journaux d’activité pendant plus de 90 jours<sup>1</sup>
- Mettre en corrélation des journaux d’activité avec d’autres données d’application et de plateforme Azure
- Consulter les activités opérationnelles regroupées par état
- Voir les tendances des activités se produisant sur chacun de vos services Azure
- Signaler les modifications d’autorisation sur toutes vos ressources Azure
- Identifier les problèmes d’intégrité de service ou de panne qui ont un impact sur vos ressources
- Utiliser des activités de recherche de journal toocorrelate utilisateur, les opérations à l’échelle automatique, les modifications d’autorisation et les journaux du service d’intégrité tooother ou les métriques à partir de votre environnement

<sup>1</sup>par défaut, Analytique de journal conserve vos journaux d’activités Windows Azure pendant 90 jours, même si vous êtes sur le niveau gratuit de hello. Ou si votre espace de travail est réglé sur une rétention de moins de 90 jours. Si votre espace de travail présente la durée de rétention de plus de 90 jours, les journaux d’activité hello sont conservés pour la période de rétention de hello de votre espace de travail.

Analytique de journal collecte des journaux d’activité gratuitement et stocke les journaux de hello pendant 90 jours gratuites. Si vous stockez les journaux pour plus de 90 jours, vous occasionnent des frais de rétention de données pour les données de hello stockées plus de 90 jours.

Lorsque vous êtes sur le niveau de tarification gratuit de hello, journaux d’activité ne s’appliquent pas la consommation de données quotidienne tooyour.

## <a name="connected-sources"></a>Sources connectées

Contrairement à la plupart des autres solutions Log Analytics, les données ne sont pas collectées pour les journaux d’activité par des agents. Toutes les données utilisées par la solution de hello proviennent directement d’Azure.

| Source connectée | Pris en charge | Description |
| --- | --- | --- |
| [Agents Windows](log-analytics-windows-agents.md) | Non | solution de Hello ne collecte pas les informations des agents de Windows. |
| [Agents Linux](log-analytics-linux-agents.md) | Non | solution de Hello ne collecte pas les informations des agents de Linux. |
| [Groupe d’administration SCOM](log-analytics-om-agents.md) | Non | solution de Hello ne collecte pas les informations des agents dans un groupe d’administration SCOM connecté. |
| [Compte Azure Storage](log-analytics-azure-storage.md) | Non | solution de Hello ne collecte pas les informations depuis le stockage Azure. |

## <a name="prerequisites"></a>Composants requis

- tooaccess informations du journal des activités Windows Azure, vous devez avoir un abonnement Azure.

## <a name="configuration"></a>Configuration

Effectuer hello suivant des solutions d’Analytique de journal d’activité étapes tooconfigure hello pour vos espaces de travail.

1. Activer la solution Analytique de journal d’activité hello hello [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureActivityOMS?tab=Overview) ou à l’aide de hello est décrite dans [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md).
2. Configurer l’espace de travail activité journaux toogo tooyour Analytique de journal.
    1. Dans hello portail Azure, sélectionnez votre espace de travail, puis sur **journal des activités Azure**.
    2. Pour chaque abonnement, cliquez sur le nom de l’abonnement hello.  
        ![ajouter un abonnement](./media/log-analytics-activity/add-subscription.png)
    3. Bonjour *SubscriptionName* panneau, cliquez sur **connexion**.  
        ![connecter un abonnement](./media/log-analytics-activity/subscription-connect.png)

Si vous ajoutez la solution hello à l’aide du portail OMS hello, vous verrez hello suivant vignette. Se connecter toohello tooconnect portail Azure un espace de travail tooyour abonnement Azure.  
![exécution de l’évaluation](./media/log-analytics-activity/tile-performing-assessment.png)

## <a name="using-hello-solution"></a>À l’aide de la solution de hello

Lorsque vous ajoutez d’espace de travail hello Analytique de journal d’activité solution tooyour, hello **journaux d’activité Azure** vignette est ajoutée le tableau de bord de présentation tooyour. Cette vignette affiche le nombre hello d’enregistrements des activités Windows Azure pour hello des abonnements Azure hello solution a accès à.

![Vignette Journaux d’activité Azure](./media/log-analytics-activity/azure-activity-logs-tile.png)

### <a name="view-azure-activity-logs"></a>Consulter des journaux d’activité Azure

Cliquez sur hello **journaux d’activité Azure** vignette tooopen hello **journaux d’activité Azure** tableau de bord. tableau de bord Hello inclut les panneaux hello Bonjour tableau suivant. Chaque panneau répertorie les articles too10 mise en correspondance que les critères du panneau pour hello spécifié plage étendue et d’heure. Vous pouvez exécuter une recherche de journal qui retourne tous les enregistrements en cliquant sur **afficher tous les** bas hello du Panneau de hello ou en cliquant sur hello panneau en-tête.

Données de journal d’activité apparaissent uniquement *après* vous avez configuré votre solution activité journaux toogo toohello, donc vous ne pouvez pas afficher les données avant cette date.

| Panneau | Description |
| --- | --- |
| Entrées de journal d’activité Azure | Affiche des totaux des enregistrements pour la plage de dates hello que vous avez sélectionné un graphique à barres de haut de hello entrée du journal des activités Windows Azure et affiche une liste de hello appelants d’activité 10 supérieure. Cliquez sur hello graphique à barres toorun une recherche de journal pour <code>Type=AzureActivity</code>. Cliquez sur un toorun d’élément appelant une recherche de journal retourner toutes les entrées de journal d’activité pour cet élément. |
| Journaux d’activité par état | Affiche un graphique en anneau pour l’état du journal des activités Windows Azure pour la plage de dates hello que vous avez sélectionné. Affiche également la liste une liste d’enregistrements d’état dix principaux hello. Cliquez sur hello graphique toorun une recherche de journal pour <code>Type=AzureActivity &#124; measure count() by ActivityStatus</code>. Cliquez sur un toorun d’élément de statut à une recherche de journal retourner toutes les entrées de journal d’activité pour cet enregistrement de l’état. |
| Journaux d’activité par ressource | Affiche le nombre total de hello de ressources avec des journaux d’activité et répertorie haut hello dénombre les dix ressources avec l’enregistrement de chaque ressource. Cliquez sur hello zone totale toorun une recherche de journal pour <code>Type=AzureActivity &#124; measure count() by Resource</code>, qui montre toutes les ressources Azure disponibles toohello solution. Cliquez sur une ressource toorun une recherche de journal retourner tous les enregistrements d’activité pour cette ressource. |
| Journaux d’activité par fournisseur de ressources | Hello affiche le nombre total de fournisseurs de ressources qui produisent activité enregistre et répertorie les dix hello. Cliquez sur hello zone totale toorun une recherche de journal pour <code>Type=AzureActivity &#124; measure count() by ResourceProvider</code>, qui montre les fournisseurs de ressources Azure. Cliquez sur un toorun de fournisseur de ressources une recherche de journal retourner tous les enregistrements d’activité pour le fournisseur de hello. |

![Tableau de bord Journaux d’activité Azure](./media/log-analytics-activity/activity-log-dash.png)

## <a name="next-steps"></a>Étapes suivantes

- Créez une [alerte](log-analytics-alerts-creating.md) lorsqu’une activité spécifique se produit.
- Utilisez [recherche de journal](log-analytics-log-searches.md) tooview détaillée des informations à partir de vos journaux d’activité.
