---
title: "Présentation d’Azure Resource Health | Microsoft Docs"
description: "Vue d’ensemble d’Azure Resource Health"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/01/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: 040d58a81a9b41fe660e4276d698bf884f90bb6c
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="azure-resource-health-overview"></a>Présentation d’Azure Resource Health
 
Resource Health vous permet d’établir des diagnostics et d’obtenir de l’aide lorsqu’un problème touchant Azure a des répercussions sur vos ressources. Il vous informe de l’intégrité (actuelle et passée) de vos ressources et vous aide à atténuer les problèmes. Resource Health propose un support technique dès lors que vous êtes confronté à des problèmes de service Azure et que vous avez besoin d’aide.

Là où le [Statut Azure](https://status.azure.com) vous informe des problèmes de service qui affectent un grand nombre de clients Azure, Resource Health vous offre un tableau de bord personnalisé de l’intégrité de vos ressources. Resource Health vous montre toutes les fois où vos ressources ont été indisponibles dans le passé en raison de problèmes de service Azure. Cela vous permet de comprendre simplement si un contrat SLA a été enfreint. 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a>Qu’est-ce qu’une ressource et comment Resource Health juge-t-il de l’intégrité d’une ressource ?
Une ressource est une instance créée par un utilisateur d’un type de ressource fourni par un service Azure via Azure Resource Manager, par exemple une machine virtuelle, une application web ou une base de données SQL.

Resource Health s’appuie sur des signaux émis par les différents services Azure pour évaluer l’intégrité d’une ressource. Si une ressource n’est pas intègre, Resource Health analyse des informations supplémentaires pour déterminer la source du problème. Il identifie également les actions adoptées par Microsoft pour résoudre le problème ou les actions que vous pouvez prendre pour résoudre la cause du problème. 

Passez en revue la liste complète de types de ressource et de vérifications d’intégrité dans [Azure Resource Health](resource-health-checks-resource-types.md) pour plus d’informations sur la procédure d’évaluation de l’intégrité.

## <a name="health-status-provided-by-resource-health"></a>L’état d’intégrité fourni par Resource Health
L’intégrité d’une ressource affiche un des états suivants :

### <a name="available"></a>Disponible
Le service n’a pas détecté d’événements ayant un impact sur l’intégrité de la ressource. Dans les cas où la ressource a récupéré d’un arrêt non planifié au cours des dernières 24 heures, vous verrez la notification **récupération récente**.

![Machine virtuelle disponible Resource Health](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a>Non disponible
Le service a détecté un événement de plateforme ou hors plateforme en cours ayant un impact sur l’intégrité de la ressource.

#### <a name="platform-events"></a>Événements de plateforme
Ces événements sont déclenchés par plusieurs composants de l’infrastructure Azure et incluent les actions planifiées telles que de la maintenance planifiée, ainsi que les incidents inattendus, comme un redémarrage non planifié de l’hôte.

Resource Health fournit des détails supplémentaires sur l’événement et le processus de récupération et vous permet de contacter le support technique même si vous n’avez pas un contrat de support technique Microsoft actif.

![Machine virtuelle indisponible Resource Health en raison d’un événement de plateforme](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a>Événements hors plateforme
Ces événements sont déclenchés par des actions effectuées par les utilisateurs, par exemple l’arrêt d’une machine virtuelle ou l’arrivée au nombre maximal de connexions à un cache Redis.

![Machine virtuelle indisponible Resource Health en raison d’un événement hors plateforme](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a>Unknown
L’état d’intégrité indique que Resource Health n’a reçu aucune information sur cette ressource depuis plus de 10 minutes. Si cet état n’est pas une indication définitive de l’état de la ressource, il s’agit d’un point de données important dans le processus de dépannage :
* Si la ressource fonctionne comme prévu, l’état de la ressource est mis à jour sur Disponible après quelques minutes.
* Si vous rencontrez des problèmes avec la ressource, l’état d’intégrité Inconnu peut suggérer que la ressource est affectée par un événement dans la plateforme.

![Machine virtuelle inconnue Resource Health](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a>Signaler un état incorrect
Si à tout moment, vous pensez que l’état actuel est incorrect, vous pouvez nous le faire savoir en cliquant sur **Signaler un état d’intégrité incorrect**. Dans le cas où vous êtes affecté par un problème avec Azure, nous vous invitons à contacter le support à partir du panneau Resource Health. 

![Signaler un état incorrect dans Resource Health](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a>Informations d’historique
Vous pouvez accéder aux données historiques d’intégrité jusqu'à 14 jours en cliquant sur **Afficher l’historique** dans le panneau de Resource Health. 

![Historique des rapports de Resource Health](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a>Prise en main
Pour ouvrir Resource Health pour une ressource
1.  Connectez-vous au portail Azure.
2.  Accédez à votre ressource.
3.  Dans le menu de ressources situé dans la partie gauche, cliquez sur **Intégrité des ressources**.

![Ouvrir Resource Health depuis le panneau Ressource](./media/resource-health-overview/from-resource-blade.png)

Vous pouvez également accéder à Resource Health en cliquant sur **Plus de services** et en saisissant **Resource Health** dans la zone de texte de filtre pour ouvrir le panneau **Aide + Support**. Cliquez enfin sur [**Intégrité des ressources**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).

![Ouvrir Resource Health depuis Plus de services](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur Resource Health, consultez les ressources suivantes :
-  [Types de ressources et les contrôles d’intégrité dans Azure Resource Health](resource-health-checks-resource-types.md)
-  [Forum aux questions sur Azure Resource Health](resource-health-faq.md)




