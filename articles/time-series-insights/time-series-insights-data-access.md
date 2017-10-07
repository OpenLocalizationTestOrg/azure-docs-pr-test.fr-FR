---
title: "aaaData des stratégies d’accès dans la série de temps Azure Insights | Documents Microsoft"
description: "Dans ce didacticiel, vous apprendre les stratégies d’accès données toomanage temps série Insights"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/01/2017
ms.author: omravi
ms.openlocfilehash: f286d26c8c5c851c523e9384760dc4b10711fa3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="grant-data-access-tooa-time-series-insights-environment-using-azure-portal"></a>Accorder l’environnement d’un aperçu en temps série tooa accès aux données à l’aide du portail Azure

Les environnements Time Series Insights comprennent deux types indépendants des stratégies d’accès :

* Stratégies d’accès de gestion
* Stratégies d’accès aux données

Ces deux stratégies accordent aux principaux Azure Active Directory (utilisateurs et applications) diverses autorisations sur un environnement spécifique. Hello principaux (utilisateurs et applications) doit appartenir toohello active directory (ou « tenant Azure ») associés à abonnement hello contenant l’environnement de hello.

Stratégies de gestion des accès accordent configuration toohello connexes d’autorisations de l’environnement de hello, telles que
*   Création et suppression de l’environnement hello, sources d’événements, référencent des jeux de données, et
*   Gestion des stratégies d’accès données hello.

Stratégies d’accès aux données accorder des autorisations tooissue des requêtes, manipulent les données de référence dans l’environnement de hello et partagent des requêtes enregistrées et perspectives associées hello environnement.

Hello deux types de stratégies d’autoriser une séparation claire entre toohello gestion de l’accès de l’environnement de hello et accéder aux données de toohello au sein de l’environnement de hello. Par exemple, il est possible toosetup un environnement telles que hello propriétaire/créateur de l’environnement de hello est supprimé de l’accès aux données hello. Ainsi que les utilisateurs et les services qui sont autorisés à tooread des données à partir de l’environnement de hello peut bénéficier sans configuration toohello d’accès de l’environnement de hello.

## <a name="grant-data-access"></a>Accorder l’accès aux données
Hello étapes suivantes montrent comment d’accès aux données de toogrant pour un utilisateur principal :

1.  Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2.  Cliquez sur « Toutes les ressources » dans le menu hello hello situé à gauche de hello portail Azure.
3.  Sélectionnez votre environnement Time Series Insights.

  ![Gérer la source de temps série Insights hello - environnement](media/data-access/getstarted-grant-data-access1.png)

4.  Sélectionnez « Accès au plan de données », puis cliquez sur « Ajouter »

  ![Gérer la source de temps série Insights hello - ajouter](media/data-access/getstarted-grant-data-access2.png)

5.  Cliquez sur « Sélectionner un utilisateur ».
6.  Recherchez et sélectionnez l’utilisateur par courrier électronique de hello.
7.  Cliquez sur « Sélectionner » dans le panneau « Sélectionner un utilisateur ».

  ![Gérer la source de temps série Insights hello - sélectionnez l’utilisateur](media/data-access/getstarted-grant-data-access3.png)

8.  Cliquez sur « Sélectionner un rôle ».
9.  Sélectionnez « Contributeur » si vous souhaitez que les données de référence toochange tooallow utilisateur et de partagez des requêtes enregistrées et perspectives avec d’autres utilisateurs de l’environnement de hello. Dans le cas contraire, sélectionner des données de requête « Lecture » tooallow utilisateur dans l’environnement de hello et enregistrer des requêtes personnelles (non partagés) dans un environnement de hello.
10. Dans le panneau de « Sélectionner un rôle » hello, cliquez sur « Ok ».

  ![Gérer la source de temps série Insights hello - sélectionner un rôle](media/data-access/getstarted-grant-data-access4.png)

11. Dans le panneau de « Rôle d’utilisateur de sélectionner » hello, cliquez sur « Ok ».
12. Ce qui suit doit s’afficher :

  ![Gérer la source de temps série Insights hello - résultats](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a>Étapes suivantes

* [Créer une source d’événement](time-series-insights-add-event-source.md)
* [Envoyer des événements](time-series-insights-send-events.md) toohello source d’événement
* Afficher votre environnement dans le [Portail Time Series Insights](https://insights.timeseries.azure.com)
