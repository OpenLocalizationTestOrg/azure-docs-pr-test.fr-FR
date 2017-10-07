---
title: "aaaGet main d’Azure Scheduler dans le portail Azure | Documents Microsoft"
description: "Prise en main d’Azure Scheduler dans le portail Azure"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: e69542ec-d10f-4f17-9b7a-2ee441ee7d68
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: deli
ms.openlocfilehash: 58255c0ad19da65932f8b1d36cb8fef1ff6e651b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a>Prise en main d’Azure Scheduler dans le portail Azure
Il est facile toocreate planifié des travaux dans Azure Scheduler. Dans ce didacticiel, vous allez apprendre comment toocreate un travail. Vous y découvrirez également les fonctionnalités de gestion et de surveillance de Scheduler.

## <a name="create-a-job"></a>Création d’un travail
1. Connectez-vous trop[portail Azure](https://portal.azure.com/).  
2. Cliquez sur **+ nouveau** > type *planificateur* dans la zone de recherche hello > sélectionnez **planificateur** dans les résultats > cliquez sur **créer**.
   
    ![][marketplace-create]
3. Nous allons créer un travail qui accède simplement à http://www.microsoft.com/ avec une demande GET. Bonjour **tâche du planificateur** écran, entrez hello informations suivantes :
   
   1. **Nom :**`getmicrosoft`  
   2. **Abonnement :** votre abonnement Azure.   
   3. **Collection de tâches :** sélectionnez une collection de tâches existante, ou cliquez sur **Créer** et entrez un nom.
4. Ensuite, dans **paramètres d’Action**, définir hello valeurs suivantes :
   
   1. **Type d’action :**` HTTP`  
   2. **Méthode :**`GET`  
   3. **URL :**` http://www.microsoft.com`  
      
      ![][action-settings]
5. Pour finir, nous allons définir une planification. travail de Hello peut être défini comme un travail ponctuel, mais nous allons sélectionner une planification périodique :
   
   1. **Récurrence** : `Recurring`
   2. **Début**: date du jour
   3. **Répéter toutes les** : `12 Hours`
   4. **Fin**: deux jours à compter de la date du jour  
      
      ![][recurrence-schedule]
6. Cliquez sur **Créer**

## <a name="manage-and-monitor-jobs"></a>Gestion et surveillance des travaux
Une fois qu’une tâche est créée, elle s’affiche dans le tableau de bord Azure hello principal. Cliquez sur le travail de hello et une nouvelle fenêtre s’ouvre avec hello suivant onglets :

1. Propriétés  
2. Paramètres d’action  
3. Planification  
4. Historique
5. Utilisateurs
   
   ![][job-overview]

### <a name="properties"></a>Propriétés
Ces propriétés en lecture seule décrivent les métadonnées de gestion hello pour la tâche du planificateur hello.

   ![][job-properties]

### <a name="action-settings"></a>Paramètres d’action
En cliquant sur un travail Bonjour **travaux** écran vous permet de tooconfigure de la tâche. Cela vous permet de configurer les paramètres avancés, si vous n’avez pas les configurer dans hello Assistant de création rapide.

Pour tous les types d’action, vous pouvez modifier la stratégie de nouvelle tentative hello et action d’erreur hello.

Pour les types d’action de tâche HTTP et HTTPS, vous pouvez modifier tooany de méthode hello autorisé le verbe HTTP. Vous pouvez également ajouter, supprimer ou modifier les en-têtes de hello et les informations d’authentification de base.

Pour les types d’action de file d’attente de stockage, vous pouvez modifier le compte de stockage hello, nom de la file d’attente, un jeton SAS et corps.

Pour les types d’action service bus, vous pouvez modifier l’espace de noms hello, chemin d’accès de rubrique/file d’attente, les paramètres d’authentification, type de transport, les propriétés de message et le corps du message.

   ![][job-action-settings]

### <a name="schedule"></a>Planification
Cela vous permet de reconfigurer la planification de hello, si vous souhaitez que la planification de hello toochange que vous avez créé dans hello Assistant de création rapide.

Il s’agit d’une opportunité toobuild [planifications complexes et périodicité avancée dans votre travail](scheduler-advanced-complexity.md)

Vous pouvez modifier la date de début hello et le temps, la planification de périodicité et hello date de fin et l’heure (si le travail de hello est périodique).

   ![][job-schedule]

### <a name="history"></a>Historique
Hello **historique** onglet affiche les métriques sélectionnées pour chaque exécution du travail dans le système hello pour la tâche sélectionnée de hello. Ces métriques fournissent des valeurs en temps réel concernant la santé de votre planificateur hello :

1. État  
2. Détails  
3. Nouvelles tentatives
4. Occurrence : 1er, 2e, 3e, etc.
5. Heure de début de l’exécution  
6. Heure de fin de l’exécution
   
   ![][job-history]

Vous pouvez cliquer sur une exécution tooview son **détails de l’historique**, y compris la réponse entière de hello pour chaque exécution. Cette boîte de dialogue vous permet également de Presse-papiers de toohello toocopy hello réponse.

   ![][job-history-details]

### <a name="users"></a>Utilisateurs
Le contrôle d’accès en fonction du rôle (RBAC) Azure permet une gestion précise de l’accès pour Azure Scheduler. toolearn comment toouse hello onglet utilisateurs, référence trop[du contrôle d’accès](../active-directory/role-based-access-control-configure.md)

## <a name="see-also"></a>Voir aussi
 [Présentation d'Azure Scheduler](scheduler-intro.md)

 [Concepts, terminologie et hiérarchie d’entités de Scheduler](scheduler-concepts-terms.md)

 [Plans et facturation dans Azure Scheduler](scheduler-plans-billing.md)

 [Comment toobuild complexe planifie et périodicité avancée avec Azure Scheduler](scheduler-advanced-complexity.md)

 [Informations de référence sur l’API REST de Scheduler](https://msdn.microsoft.com/library/mt629143)

 [Informations de référence sur les applets de commande PowerShell de Scheduler](scheduler-powershell-reference.md)

 [Haute disponibilité et fiabilité de Scheduler](scheduler-high-availability-reliability.md)

 [Limites, valeurs par défaut et codes d’erreur de Scheduler](scheduler-limits-defaults-errors.md)

 [Authentification sortante de Scheduler](scheduler-outbound-authentication.md)

[marketplace-create]: ./media/scheduler-get-started-portal/scheduler-v2-portal-marketplace-create.png
[action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-action-settings.png
[recurrence-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-recurrence-schedule.png
[job-properties]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-properties.png
[job-overview]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-overview-1.png
[job-action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-action-settings.png
[job-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-schedule.png
[job-history]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history.png
[job-history-details]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history-details.png


[1]: ./media/scheduler-get-started-portal/scheduler-get-started-portal001.png
[2]: ./media/scheduler-get-started-portal/scheduler-get-started-portal002.png
[3]: ./media/scheduler-get-started-portal/scheduler-get-started-portal003.png
[4]: ./media/scheduler-get-started-portal/scheduler-get-started-portal004.png
[5]: ./media/scheduler-get-started-portal/scheduler-get-started-portal005.png
[6]: ./media/scheduler-get-started-portal/scheduler-get-started-portal006.png
[7]: ./media/scheduler-get-started-portal/scheduler-get-started-portal007.png
[8]: ./media/scheduler-get-started-portal/scheduler-get-started-portal008.png
[9]: ./media/scheduler-get-started-portal/scheduler-get-started-portal009.png
[10]: ./media/scheduler-get-started-portal/scheduler-get-started-portal010.png
[11]: ./media/scheduler-get-started-portal/scheduler-get-started-portal011.png
[12]: ./media/scheduler-get-started-portal/scheduler-get-started-portal012.png
[13]: ./media/scheduler-get-started-portal/scheduler-get-started-portal013.png
[14]: ./media/scheduler-get-started-portal/scheduler-get-started-portal014.png
[15]: ./media/scheduler-get-started-portal/scheduler-get-started-portal015.png
