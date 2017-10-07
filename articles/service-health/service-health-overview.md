---
title: "vue d’ensemble de l’intégrité du Service aaaAzure | Documents Microsoft"
description: "Obtenez des informations personnalisées concernant l’incidence des problèmes et de la maintenance actuels et futurs d’Azure sur vos applications Azure."
services: Resource health
documentationcenter: 
author: rboucher
manager: 
editor: 
ms.assetid: 
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/07/2017
ms.author: robb
ms.openlocfilehash: 2b536ee2f19757d4f2baf5529866c3d159a4670c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-health"></a>Azure Service Health
Azure Service Health fournit en temps voulu des informations personnalisées lorsque des problèmes touchant les services Azure ont une incidence sur vos services.  Cette fonctionnalité vous aide également à vous préparer aux maintenances planifiées à venir.

## <a name="service-health-events"></a>Événements Service Health
Service Health suit trois types d’événements d’intégrité qui peuvent avoir une incidence sur vos ressources :
1. **Problèmes de service** -des problèmes dans hello des services Azure que vous dès maintenant. 
2. **Une maintenance planifiée** -maintenance à venir qui peut affecter la disponibilité de hello de vos services Bonjour futures.  
3. **Health advisories** (Avis concernant l’intégrité) : modifications apportées aux services Azure qui nécessitent votre attention. Ce type d’événement se produit par exemple lorsque des fonctionnalités Azure sont déconseillées ou si vous dépassez un quota d’utilisation.

    ![Événements Service Health](./media/service-health-overview/azure-service-health-overview-7.png)

## <a name="get-started-with-service-health"></a>Prise en main de Service Health
toolaunch vignette de votre tableau de bord d’intégrité du Service, sélectionnez hello l’intégrité du Service sur votre tableau de bord de portail. Si vous avez précédemment supprimé la vignette de hello ou si vous utilisez le tableau de bord personnalisé, de recherche pour le service de contrôle d’intégrité du Service dans « Plus services » (en bas à gauche sur votre tableau de bord).
![Prise en main de Service Health](./media/service-health-overview/azure-service-health-overview-1.png)

## <a name="see-current-issues-which-impact-your-services"></a>Afficher les problèmes actuels qui ont une incidence sur vos services
Hello **problèmes des services** affiche tous les problèmes en cours dans les services Azure qui affectent vos ressources. Vous pouvez comprendre quand le problème de hello a commencé et que les services et les régions sont affectées. Vous pouvez également lire toounderstand mise à jour de la plus récente hello qu’Azure effectue un problème de hello tooresolve. 
![Gestion des problèmes liés au service](./media/service-health-overview/azure-service-health-overview-2.png)

Choisissez hello **impact potentiel** liste spécifique de hello toosee onglet ressources peuvent être impactés par problème de hello. Vous pouvez télécharger une liste CSV de tooshare de ces ressources avec votre équipe.
![Gestion des problèmes liés au service - Impact](./media/service-health-overview/azure-service-health-overview-4.png)

## <a name="get-links-and-downloadable-explanations"></a>Obtenir des liens et des explications téléchargeables 
Vous pouvez obtenir un lien pour hello problème toouse dans votre système de gestion du problème. Vous pouvez télécharger le PDF et parfois tooshare de fichiers CSV avec des personnes qui n’ont pas accès toohello portail Azure.   
![Gestion des problèmes liés aux services - Gestion des problèmes](./media/service-health-overview/azure-service-health-overview-3.png)

## <a name="get-support-from-microsoft"></a>Obtenir l’aide du support Microsoft
Contactez le support technique si votre ressource n’est pas dans un état incorrect, même après que hello problème est résolu.  Utilisez les liens de prise en charge de hello sur hello à droite de la page de hello.  

## <a name="pin-a-personalized-health-map-tooyour-dashboard"></a>Épingler un tableau de bord d’intégrité personnalisé carte tooyour
Filtrer l’intégrité du Service tooshow vos abonnements critiques, les régions et les types de ressources. Enregistrer le filtre de hello et code confidentiel un contrôle d’intégrité personnalisé world carte tooyour portail tableau de bord. 
![Filtrer une carte d’intégrité personnalisée](./media/service-health-overview/azure-service-health-overview-6a.png)
![Épingler une carte d’intégrité personnalisée](./media/service-health-overview/azure-service-health-overview-6b.png)

## <a name="configure-service-health-alerts"></a>Configurer des alertes Service Health
L’intégrité du Service Azure s’intègre à Azure moniteur tooalert vous via des messages électroniques, les messages texte et les notifications de webhook lorsque vos ressources critiques sont affectés. Configurer une alerte de journal d’activité pour les événements d’intégrité du Service approprié hello. Itinéraire toohello les personnes appropriées dans votre organisation à l’aide de groupes d’actions d’alerte. Pour plus d’informations sur la configuration d’alertes pour Service Health, consultez [cet article](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md).

# <a name="next-steps"></a>Étapes suivantes
Configurez des alertes afin d’être averti des problèmes d’intégrité. Pour plus d’informations sur la configuration d’alertes pour Service Health, consultez [cet article](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md). 