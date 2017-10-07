---
title: "vue d’ensemble du contrôle d’intégrité de ressource aaaAzure | Documents Microsoft"
description: "Vue d’ensemble d’Azure Resource Health"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: resource-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 06/01/2016
ms.author: BernardoAMunoz
ms.openlocfilehash: b920241b2f64a0695ba2c32e9ccb0c2c3739986d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-overview"></a>Présentation d’Azure Resource Health
 
Resource Health vous permet d’établir des diagnostics et d’obtenir de l’aide lorsqu’un problème touchant Azure a des répercussions sur vos ressources. Il vous informe de la santé de vos ressources hello actuelles et passées et vous permet d’atténuer les problèmes. Resource Health propose un support technique dès lors que vous êtes confronté à des problèmes de service Azure et que vous avez besoin d’aide.

Alors que [Azure Status](https://status.azure.com) vous informe des problèmes de service qui affectent un large éventail de clients Azure, l’intégrité des ressources vous offre un tableau de bord personnalisé d’intégrité hello de vos ressources. L’intégrité des ressources vous montre toutes les heures hello vos ressources n’étaient pas disponibles dans hello passé en raison de problèmes de service tooAzure. Cela rend simple pour vous toounderstand si un contrat SLA a été violé. 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a>Qu’est-ce qu’une ressource et comment Resource Health juge-t-il de l’intégrité d’une ressource ?
Une ressource est une instance créée par un utilisateur d’un type de ressource fourni par un service Azure via Azure Resource Manager, par exemple une machine virtuelle, une application web ou une base de données SQL.

L’intégrité des ressources s’appuie sur des signaux émis par hello différents services Azure tooassess si une ressource est saine ou non. Si une ressource est défectueux, l’intégrité des ressources analyse les informations supplémentaires toodetermine hello source hello problème. Il identifie également les actions que Microsoft prend toofix hello problème ou faire ce qui les actions à entreprendre tooaddress hello provoquent de problème de hello. 

Révision hello la liste complète des types de ressources et d’intégrité vérifie [l’intégrité des ressources Azure](resource-health-checks-resource-types.md) pour plus d’informations sur la procédure d’évaluation d’intégrité.

## <a name="health-status-provided-by-resource-health"></a>L’état d’intégrité fourni par Resource Health
intégrité Hello d’une ressource est un des hello suivant des États :

### <a name="available"></a>Disponible
service de Hello n’a détecté que tous les événements ayant un impact sur l’intégrité de hello de ressource de hello. Dans les cas où les ressources hello a récupéré de temps d’arrêt non planifié pendant hello dernières 24 heures, vous verrez hello **récemment récupéré** notification.

![Machine virtuelle disponible Resource Health](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a>Non disponible
service de Hello a détecté une plateforme en cours ou un événement non-plateforme ayant un impact sur l’intégrité de hello de ressource de hello.

#### <a name="platform-events"></a>Événements de plateforme
Ces événements sont déclenchés par plusieurs composants de hello infrastructure Azure et incluent les actions planifiées telles que de maintenance planifiée et des incidents inattendues comme un redémarrage de l’ordinateur hôte non planifié.

L’intégrité des ressources fournit des détails supplémentaires sur l’événement hello, processus de récupération hello et vous permet la prise en charge de toocontact même si vous n’avez pas de contrat de support technique d’un Microsoft actif.

![Ressource d’intégrité indisponible virtual machine en raison de l’événement de tooplatform](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a>Événements hors plateforme
Ces événements sont déclenchés par les actions effectuées par les utilisateurs, par exemple l’arrêt d’un ordinateur virtuel ou atteindre hello le nombre maximal de connexions tooa Cache Redis.

![Ressource d’intégrité indisponible virtual machine en raison de l’événement de plate-forme de toonon](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a>Unknown
L’état d’intégrité indique que Resource Health n’a reçu aucune information sur cette ressource depuis plus de 10 minutes. Cet état n’est pas une indication définitive de l’état hello de ressource de hello, il est un point de données importantes dans hello processus de dépannage :
* Si les ressources hello sont en cours d’exécution en tant qu’état hello attendu de ressource de hello met à jour tooAvailable après quelques minutes.
* Si vous rencontrez des problèmes avec les ressources hello, hello état d’intégrité inconnu peut suggérer la ressource de hello est affectée par un événement de plate-forme de hello.

![Machine virtuelle inconnue Resource Health](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a>Signaler un état incorrect
Si à tout moment, vous pensez état d’intégrité actuel de hello est incorrect, vous pouvez faites-le nous savoir en cliquant sur **signaler l’état d’intégrité incorrect**. Dans les cas où vous n’êtes affecté à un problème d’Azure, nous vous encourageons prise en charge toocontact à partir du Panneau de contrôle d’intégrité des ressources hello. 

![Signaler un état incorrect dans Resource Health](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a>Informations d’historique
Vous pouvez accéder à des jours too14 des données historiques d’intégrité en cliquant sur **afficher l’historique** dans le panneau de contrôle d’intégrité des ressources hello. 

![Historique des rapports de Resource Health](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a>Prise en main
tooopen l’intégrité des ressources pour une ressource
1.  Connectez-vous en hello portail Azure.
2.  Accédez tooyour ressource.
3.  Dans le menu de ressource hello situé dans la partie gauche hello, cliquez sur **l’intégrité des ressources**.

![Ouvrir Resource Health depuis le panneau Ressource](./media/resource-health-overview/from-resource-blade.png)

Vous pouvez également accéder à l’intégrité des ressources en cliquant sur **davantage de services**et en tapant **l’intégrité des ressources** Bonjour de tooopen de zone de texte filtre **aide et Support** panneau. Cliquez enfin sur [**Intégrité des ressources**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).

![Ouvrir Resource Health depuis Plus de services](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a>Étapes suivantes

Passez en revue ces toolearn de ressources en savoir plus sur l’intégrité des ressources :
-  [Types de ressources et les contrôles d’intégrité dans Azure Resource Health](resource-health-checks-resource-types.md)
-  [Forum aux questions sur Azure Resource Health](resource-health-faq.md)




