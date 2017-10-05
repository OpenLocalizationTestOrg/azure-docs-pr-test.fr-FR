---
title: "Surveiller l’intégrité et les alertes dans Azure Stack | Microsoft Docs"
description: "Découvrez comment surveiller l’intégrité et les alertes dans Azure Stack."
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
ms.openlocfilehash: 93835eabcf9622735aada0f5dfa46028553c25bd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="monitor-health-and-alerts-in-azure-stack"></a>Surveiller l’intégrité et les alertes dans Azure Stack

Azure Stack inclut des fonctionnalités de surveillance de l’infrastructure qui permettent à un opérateur cloud de visualiser les alertes et l’intégrité d’une région Azure Stack.

Azure Stack dispose d’un ensemble de fonctionnalités de gestion des régions disponibles dans la vignette **Gestion des régions**. Cette vignette, épinglée par défaut dans le portail administrateur de l’abonnement Fournisseur par défaut, répertorie toutes les régions déployées d’Azure Stack. Elle montre également le nombre d’alertes critiques et d’avertissement actifs pour chaque région. Cette vignette est votre point d’entrée vers la fonctionnalité d’alerte et d’intégrité d’Azure Stack.

 ![Vignette Gestion des régions](media/azure-stack-monitor-health/image1.png)

 ## <a name="understand-health-in-azure-stack"></a>Présentation de l’intégrité dans Azure Stack

 L’intégrité et les alertes sont gérées dans Azure Stack par le fournisseur de ressources Intégrité. Les composants d’infrastructure Azure Stack s’inscrivent auprès du fournisseur de ressources Intégrité lors du déploiement et de la configuration d’Azure Stack. Cette inscription permet de visualiser l’intégrité et les alertes pour chaque composant. L’intégrité dans Azure Stack est un concept simple. S’il existe des alertes pour une instance inscrite d’un composant, l’état d’intégrité de ce composant reflète la gravité de l’alerte active la plus sévère : avertissement ou critique.
 
 ## <a name="view-and-manage-component-health-state"></a>Afficher et gérer l’état d’intégrité des composants
 
 Vous pouvez afficher l’état d’intégrité des composants dans le portail administrateur d’Azure Stack et par le biais des API Rest et de PowerShell.
 
Pour afficher l’état d’intégrité dans le portail, cliquez sur la région que vous souhaitez visualiser dans la vignette **Gestion des régions**. Vous pouvez afficher l’état d’intégrité des rôles d’infrastructure et des fournisseurs de ressources. Notez que dans cette version, le fournisseur de ressources Calcul ne signale pas l’état d’intégrité.

![Liste des rôles d’infrastructure](media/azure-stack-monitor-health/image2.png)

Vous pouvez cliquer sur un fournisseur de ressources ou un rôle d’infrastructure pour afficher des informations plus détaillées.

> [!WARNING]
>Si vous cliquez sur un rôle d’infrastructure puis sur l’instance de rôle, des options Démarrer, Redémarrer ou Arrêter s’affichent dans le panneau **Instance de rôle**. N’utilisez **pas** ces options dans un environnement du Kit de développement Azure Stack. Elles sont conçues uniquement pour un environnement à plusieurs nœuds, où il existe plusieurs instances de rôle par rôle d’infrastructure. Le redémarrage d’une instance de rôle (notamment AzS-Xrp01) dans le Kit de développement entraîne une instabilité du système. Pour obtenir une assistance en cas de problème, postez votre problème sur le [Forum Azure Stack](https://aka.ms/azurestackforum).
>
 
## <a name="view-alerts"></a>Afficher les alertes

La liste des alertes actives pour chaque région Azure Stack est disponible directement à partir du panneau **Gestion des régions**. La première vignette dans la configuration par défaut est la vignette **Alertes**, qui fournit un récapitulatif des alertes critiques et des avertissements pour la région. Vous pouvez épingler la vignette Alertes au tableau de bord (comme n’importe quelle autre vignette sur ce panneau) pour pouvoir y accéder rapidement.   

![Vignette Alertes qui affiche un avertissement](media/azure-stack-monitor-health/image3.png)

En sélectionnant la partie supérieure de la vignette **Alertes**, vous accédez à la liste de toutes les alertes actives pour la région. Si vous sélectionnez l’élément de ligne **Critique** ou **Avertissement** dans la vignette, vous accédez à une liste filtrée des alertes (Critique ou Avertissement). 

![Avertissements filtrés](media/azure-stack-monitor-health/image4.png)
  
Le panneau **Alertes** prend en charge la possibilité de filtrer à la fois sur le niveau de gravité (Critique ou Avertissement) et sur l’état (Actif ou Fermé). L’affichage par défaut montre toutes les alertes actives. Toutes les alertes fermées sont supprimées du système après sept jours.

![Volet Filtre pour filtrer par état Critique ou Avertissement](media/azure-stack-monitor-health/image5.png)

Le panneau Alertes expose également l’action **API de vue**, qui montre l’API Rest utilisée pour générer la vue de liste. Cette action permet de se familiariser rapidement avec la syntaxe d’API Rest que vous pouvez utiliser pour interroger les alertes. Vous pouvez utiliser cette API dans l’automation ou pour l’intégration avec vos solutions existantes de création de tickets, de création de rapports et de surveillance de centre de données. 

![L’option API de vue qui montre l’API Rest](media/azure-stack-monitor-health/image6.png)

Dans le panneau Alertes, vous pouvez sélectionner une alerte pour accéder au panneau **Détails de l’alerte**. Ce panneau affiche tous les champs associés à l’alerte, et permet d’accéder rapidement au composant affecté et à la source de l’alerte. Par exemple, l’alerte suivante se produit si l’une des instances de rôle d’infrastructure bascule hors connexion ou est inaccessible.  

![Le panneau Détails de l’alerte](media/azure-stack-monitor-health/image7.png)

Une fois l’instance de rôle d’infrastructure de nouveau en ligne, cette alerte se ferme automatiquement.

## <a name="next-steps"></a>Étapes suivantes

[Gérer les mises à jour dans Azure Stack](azure-stack-updates.md)

[Gestion des régions dans Azure Stack](azure-stack-region-management.md)
