---
title: "aaaMonitor contrôle d’intégrité et des alertes dans la pile de Azure | Documents Microsoft"
description: "Découvrez comment toomonitor contrôle d’intégrité et des alertes dans la pile de Azure."
services: azure-stack
documentationcenter: 
author: chasat-MS
manager: dsavage
editor: 
ms.assetid: 69901c7b-4673-4bd8-acf2-8c6bdd9d1546
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: chasat
ms.openlocfilehash: 11e287c497e154b767c775fe4afcc78ec9e72fb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-health-and-alerts-in-azure-stack"></a>Surveiller l’intégrité et les alertes dans Azure Stack

Pile Azure inclut des fonctionnalités qui permettent à un cloud opérateur tooview d’état et les alertes pour une région de la pile de Azure de surveillance de l’infrastructure.

Pile Azure possède un ensemble de fonctionnalités de gestion de la région disponibles Bonjour **gestion de la région** vignette. Cette vignette épinglée par défaut dans le portail d’administration hello pour hello abonnement du fournisseur par défaut, répertorie toutes les régions hello déployée de la pile de Azure. Il montre également le nombre de hello des alertes actives critiques et d’avertissement pour chaque région. Cette vignette est votre point d’entrée dans le contrôle d’intégrité hello et la fonctionnalité d’alerte de la pile de Azure.

 ![vignette de gestion de la région de Hello](media/azure-stack-monitor-health/image1.png)

 ## <a name="understand-health-in-azure-stack"></a>Présentation de l’intégrité dans Azure Stack

 Contrôle d’intégrité et les alertes sont gérés dans la pile d’Azure par le fournisseur de ressources hello d’intégrité. Composants d’infrastructure Azure pile inscrivent avec le fournisseur de ressources de contrôle d’intégrité hello lors du déploiement de la pile d’Azure et de configuration. Cette inscription permet l’affichage hello de contrôle d’intégrité et les alertes pour chaque composant. L’intégrité dans Azure Stack est un concept simple. Si les alertes pour une instance enregistrée d’existent un composant, hello état d’intégrité de ce composant reflète hello pire active gravité d’alerte ; avertissement ou critique.
 
 ## <a name="view-and-manage-component-health-state"></a>Afficher et gérer l’état d’intégrité des composants
 
 Vous pouvez afficher hello état des composants dans les deux portail d’administration Azure pile hello et via les API Rest et PowerShell.
 
l’état d’intégrité tooview hello dans le portail hello, cliquez sur la région hello que vous souhaitez tooview Bonjour **gestion de la région** vignette. Vous pouvez afficher l’état d’intégrité hello de rôles d’infrastructure et des fournisseurs de ressources. Notez que dans cette version, fournisseur de ressources de calcul hello ne signale pas l’état d’intégrité.

![Liste des rôles d’infrastructure](media/azure-stack-monitor-health/image2.png)

Vous pouvez cliquer sur une ressource des tooview rôle fournisseur ou d’infrastructure des informations plus détaillées.

> [!WARNING]
>Si vous cliquez sur un rôle d’infrastructure, puis cliquez sur instance de rôle hello, il existe des options Bonjour **instance de rôle** panneau tooStart, redémarrage ou arrêt. N’utilisez **pas** ces options dans un environnement du Kit de développement Azure Stack. Ces options sont conçues uniquement pour un environnement à plusieurs nœuds, où il existe plusieurs instances de rôle par rôle d’infrastructure. Le redémarrage d’une instance de rôle (notamment AzS Xrp01) dans le kit de développement hello provoque l’instabilité du système. Pour la résolution des problèmes d’assistance, publiez votre toohello problème [Forum sur la pile de Azure](https://aka.ms/azurestackforum).
>
 
## <a name="view-alerts"></a>Afficher les alertes

liste de Hello d’alertes actives pour chaque région de la pile de Azure est disponible directement à partir de hello **gestion de la région** panneau. première vignette dans la configuration par défaut de hello Hello est hello **alertes** vignette, qui affiche un résumé des alertes d’avertissement pour la région de hello hello critiques. Vous pouvez épingler la vignette d’alertes hello, comme n’importe quelle autre vignette sur ce panneau, toohello le tableau de bord pour un accès rapide.   

![Vignette Alertes qui affiche un avertissement](media/azure-stack-monitor-health/image3.png)

En sélectionnant la partie supérieure de hello Hello **alertes** vignette, vous accédez liste toohello de toutes les alertes actives pour la région de hello. Si vous sélectionnez soit hello **critique** ou **avertissement** ligne de commande dans la vignette de hello, vous accédez tooa filtré la liste des alertes (critique ou avertissement). 

![Avertissements filtrés](media/azure-stack-monitor-health/image4.png)
  
Hello **alertes** lame prend en charge hello capacité toofilter à la fois sur le niveau de gravité (critique ou avertissement) et l’état (actif ou fermé). par défaut Hello affiche toutes les alertes actives. Toutes les alertes fermées sont supprimés à partir du système de hello bout de sept jours.

![Toofilter de volet de filtre en état critique ou d’avertissement](media/azure-stack-monitor-health/image5.png)

panneau d’alertes Hello expose également hello **vue API** action, qui permet d’afficher le hello affiche les API Rest qui était la liste de hello toogenerate utilisé. Cette action fournit un moyen rapide de toobecome familiarisé avec la syntaxe d’API Rest hello que vous pouvez utiliser les alertes tooquery. Vous pouvez utiliser cette API dans l’automation ou pour l’intégration avec vos solutions existantes de création de tickets, de création de rapports et de surveillance de centre de données. 

![Hello option API de vue qui affiche hello API Rest](media/azure-stack-monitor-health/image6.png)

À partir du panneau d’alertes hello, vous pouvez sélectionner un toohello alerte toonavigate **détails de l’alerte** panneau. Ce panneau affiche tous les champs associés à l’alerte de hello, et permet une navigation rapide toohello affecté composant et source d’alerte de hello. Par exemple, hello alerte suivante se produit si une des instances de rôle d’infrastructure hello est mis hors connexion ou n’est pas accessible.  

![Panneau de détails de l’alerte Hello](media/azure-stack-monitor-health/image7.png)

Une fois l’instance de rôle d’infrastructure hello en ligne, cette alerte se ferme automatiquement.

## <a name="next-steps"></a>Étapes suivantes

[Gérer les mises à jour dans Azure Stack](azure-stack-updates.md)

[Gestion des régions dans Azure Stack](azure-stack-region-management.md)
