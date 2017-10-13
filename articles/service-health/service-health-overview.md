---
title: "Présentation d’Azure Service Health | Microsoft Docs"
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
ms.openlocfilehash: 001dc1fa2a0fd7e132101944a87be3f8552d8738
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="azure-service-health"></a>Azure Service Health
Azure Service Health fournit en temps voulu des informations personnalisées lorsque des problèmes touchant les services Azure ont une incidence sur vos services.  Cette fonctionnalité vous aide également à vous préparer aux maintenances planifiées à venir.

## <a name="service-health-events"></a>Événements Service Health
Service Health suit trois types d’événements d’intégrité qui peuvent avoir une incidence sur vos ressources :
1. **Problèmes liés aux services** : problèmes touchant les services Azure qui vous affectent en ce moment même. 
2. **Maintenance planifiée** : maintenance à venir qui pourra avoir une incidence sur la disponibilité de vos services.  
3. **Health advisories** (Avis concernant l’intégrité) : modifications apportées aux services Azure qui nécessitent votre attention. Ce type d’événement se produit par exemple lorsque des fonctionnalités Azure sont déconseillées ou si vous dépassez un quota d’utilisation.

    ![Événements Service Health](./media/service-health-overview/azure-service-health-overview-7.png)

## <a name="get-started-with-service-health"></a>Prise en main de Service Health
Pour lancer votre tableau de bord Service Health, sélectionnez la vignette Service Health dans le tableau de bord du portail. Si vous avez supprimé la vignette ou utilisez un tableau de bord personnalisé, recherchez Service Health dans Plus de services (en bas à gauche de votre tableau de bord).
![Prise en main de Service Health](./media/service-health-overview/azure-service-health-overview-1.png)

## <a name="see-current-issues-which-impact-your-services"></a>Afficher les problèmes actuels qui ont une incidence sur vos services
La vue **Problèmes liés aux services** affiche tous les problèmes touchant actuellement les services Azure qui ont une incidence sur vos ressources. Vous pouvez savoir quand le problème a commencé et quels services et régions sont concernés. Vous pouvez également accéder aux informations les plus récentes pour comprendre ce qui est fait pour résoudre le problème. 
![Gestion des problèmes liés au service](./media/service-health-overview/azure-service-health-overview-2.png)

Choisissez l’onglet **Impact potentiel** pour afficher la liste spécifique des ressources que vous détenez pouvant être affectées par le problème. Vous pouvez télécharger une liste au format CSV de ces ressources pour la partager avec votre équipe.
![Gestion des problèmes liés au service - Impact](./media/service-health-overview/azure-service-health-overview-4.png)

## <a name="get-links-and-downloadable-explanations"></a>Obtenir des liens et des explications téléchargeables 
Vous pouvez obtenir un lien pour le problème afin de l’utiliser dans votre système de gestion des problèmes. Vous pouvez télécharger des fichiers PDF et parfois CSV pour les partager avec des collaborateurs qui n’ont pas accès au portail Azure.   
![Gestion des problèmes liés aux services - Gestion des problèmes](./media/service-health-overview/azure-service-health-overview-3.png)

## <a name="get-support-from-microsoft"></a>Obtenir l’aide du support Microsoft
Contactez le support si votre ressource présente encore un état incorrect après la résolution du problème.  Utilisez les liens de support sur la droite de la page.  

## <a name="pin-a-personalized-health-map-to-your-dashboard"></a>Épingler une carte d’intégrité personnalisée à votre tableau de bord
Filtrez Service Health pour afficher vos abonnements, régions et types de ressources stratégiques. Enregistrez le filtre et épinglez une carte mondiale d’intégrité personnalisée à votre tableau de bord du portail. 
![Filtrer une carte d’intégrité personnalisée](./media/service-health-overview/azure-service-health-overview-6a.png)
![Épingler une carte d’intégrité personnalisée](./media/service-health-overview/azure-service-health-overview-6b.png)

## <a name="configure-service-health-alerts"></a>Configurer des alertes Service Health
Azure Service Health s’intègre avec Azure Monitor pour vous avertir au moyen de courriers, de SMS et de notifications webhook quand certaines de vos ressources stratégiques sont affectées. Configurez une alerte de journal d’activité pour l’événement Service Health approprié. Acheminez cette alerte aux personnes appropriées de votre organisation à l’aide de groupes d’actions. Pour plus d’informations sur la configuration d’alertes pour Service Health, consultez [cet article](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md).

# <a name="next-steps"></a>Étapes suivantes
Configurez des alertes afin d’être averti des problèmes d’intégrité. Pour plus d’informations sur la configuration d’alertes pour Service Health, consultez [cet article](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md). 