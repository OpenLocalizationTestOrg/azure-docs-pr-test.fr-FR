---
title: aaaUse toomanage portail Azure ressources Azure | Documents Microsoft
description: "Utiliser le portail Azure et gérer les ressources Azure de toomanage vos ressources. Montre comment toowork avec des ressources toomonitor de tableaux de bord."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0725bbf2-5913-4c07-af6e-24e11d957fbc
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 0c89a197a31c5b6dd03ba457cb4d1fdf9f6d00f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-resources-through-portal"></a>Gérer les ressources Azure sur le portail
> [!div class="op_single_selector"]
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [Interface de ligne de commande Azure](xplat-cli-azure-resource-manager.md)
> * [Portail](resource-group-portal.md) 
> * [API REST](resource-manager-rest-api.md)
> 
> 

Cette rubrique montre comment toouse hello [portail Azure](https://portal.azure.com) avec [Azure Resource Manager](resource-group-overview.md) toomanage vos ressources Azure. toolearn sur le déploiement de ressources via le portail de hello, consultez [déployer des ressources avec des modèles de gestionnaire de ressources et le portail Azure](resource-group-template-deploy-portal.md).

Actuellement, pas tous les services prend en charge le portail de hello ou Gestionnaire de ressources. Pour ces services, vous devez toouse hello [portail classic](https://manage.windowsazure.com). Statut de hello de chaque service, consultez [graphique de la disponibilité de portail Azure](https://azure.microsoft.com/features/azure-portal/availability/).

## <a name="manage-resource-groups"></a>Gérer des groupes de ressources

Un groupe de ressources est un conteneur réunissant les ressources associées d’une solution Azure. groupe de ressources Hello peut inclure toutes les ressources de hello pour les solutions hello, ou uniquement les ressources que vous souhaitez toomanage en tant que groupe. Vous décidez comment vous souhaitez que les ressources de tooallocate tooresource groupes en fonction de ce que hello plus logique pour votre organisation. En règle générale, ajouter des ressources qui partagent hello même cycle de vie toohello même ressource de groupe afin de pouvoir facilement déployer, mettre à jour et les supprimer en tant que groupe. 

groupe de ressources Hello stocke les métadonnées sur les ressources de hello. Par conséquent, lorsque vous spécifiez un emplacement pour le groupe de ressources hello, vous spécifiez que les métadonnées de stockage. Pour des raisons de compatibilité, vous devrez peut-être tooensure que vos données sont stockées dans une région particulière.

1. toosee tous les groupes de ressources de hello dans votre abonnement, sélectionnez **groupes de ressources**.
   
    ![parcourir les groupes de ressources](./media/resource-group-portal/browse-groups.png)
2. toocreate un groupe de ressources vide, sélectionnez **ajouter**.
   
    ![ajouter un groupe de ressources](./media/resource-group-portal/add-resource-group.png)
3. Fournissez un nom et un emplacement pour le nouveau groupe de ressources hello. Sélectionnez **Créer**.
   
    ![Créer un groupe de ressources](./media/resource-group-portal/create-empty-group.png)
4. Vous devrez peut-être tooselect **Actualiser** groupe de ressources toosee hello récemment créé.
   
    ![actualiser un groupe de ressources](./media/resource-group-portal/refresh-resource-groups.png)
5. toocustomize hello afficher les informations sur vos groupes de ressources, sélectionnez **colonnes**.
   
    ![personnaliser des colonnes](./media/resource-group-portal/select-columns.png)
6. Sélectionnez hello colonnes tooadd, puis **mise à jour**.
   
    ![ajouter des colonnes](./media/resource-group-portal/add-columns.png)
7. toolearn sur le déploiement de ressources tooyour nouveau groupe de ressources, consultez [déployer des ressources avec des modèles de gestionnaire de ressources et le portail Azure](resource-group-template-deploy-portal.md).
8. Accès rapide tooa groupe de ressources, vous pouvez épingler tooyour du tableau de bord panneau hello.
   
    ![épingler un groupe de ressources](./media/resource-group-portal/pin-group.png)
9. tableau de bord Hello affiche le groupe de ressources hello et ses ressources. Vous pouvez sélectionner des groupes de ressources hello ou un de ses éléments de toohello toonavigate ressources.
   
    ![épingler un groupe de ressources](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a>Baliser des ressources
Vous pouvez appliquer des balises tooresource groupes et ressources toologically organiser vos éléments multimédias. Pour plus d’informations sur l’utilisation des balises, consultez [à l’aide des balises tooorganize vos ressources Azure](resource-group-using-tags.md).

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a>Surveiller les ressources
Lorsque vous sélectionnez une ressource, le panneau des ressources hello présente graphiques par défaut et les tables pour l’analyse de ce type de ressource.

1. Sélectionnez un Bonjour ressource et notez **analyse** section. Elle inclut des graphiques qui sont de type de ressource toohello pertinentes. Hello image suivante montre les données pour un compte de stockage de surveillance de la valeur par défaut hello.
   
    ![afficher la surveillance](./media/resource-group-portal/show-monitoring.png)
2. Vous pouvez épingler une section du tableau de bord hello panneau tooyour en sélectionnant les points de suspension hello (...) au-dessus de la section de hello. Vous pouvez également personnaliser hello taille hello section dans le panneau de hello ou supprimez-le complètement. Hello image suivante montre comment toopin, personnaliser ou supprimer hello du processeur et la section de mémoire.
   
    ![épingler une section](./media/resource-group-portal/pin-cpu-section.png)
3. Après épinglage de tableau de bord toohello hello section, vous verrez hello résumé sur le tableau de bord hello. Et, sélectionnez-le immédiatement toomore des détails concernant hello.
   
    ![afficher le tableau de bord](./media/resource-group-portal/view-startboard.png)
4. toocompletely personnaliser les surveiller via le portail de hello, accédez tooyour du tableau de bord par défaut, puis sélectionnez les données de salutation **nouveau tableau de bord**.
   
    ![dashboard](./media/resource-group-portal/dashboard.png)
5. Donnez un nom à votre nouveau tableau de bord et faites glisser les mosaïques sur le tableau de bord hello. les vignettes de Hello sont filtrés par les différentes options.
   
    ![dashboard](./media/resource-group-portal/create-dashboard.png)
   
     toolearn sur l’utilisation des tableaux de bord, consultez [de création et de partage de tableaux de bord Bonjour Azure portal](../azure-portal/azure-portal-dashboards.md).

## <a name="manage-resources"></a>Gestion des ressources
Dans le panneau hello pour une ressource, vous voyez les options hello pour la gestion des ressources de hello. portail de Hello présente les options de gestion pour ce type de ressource spécifique. Vous consultez les commandes de gestion hello haut hello du panneau des ressources hello et sur le côté gauche de hello.

![Gestion des ressources](./media/resource-group-portal/manage-resources.png)

À partir de ces options, vous pouvez effectuer des opérations telles que le démarrage et l’arrêt d’un ordinateur virtuel ou le reconfigurer les propriétés de hello de machine virtuelle de hello.

## <a name="move-resources"></a>Déplacer des ressources
Si vous avez besoin de groupe de ressources toomove ressources tooanother ou un autre abonnement, consultez [déplacer le groupe de ressources toonew ressources ou d’un abonnement](resource-group-move-resources.md).

## <a name="lock-resources"></a>Verrouiller des ressources
Vous pouvez verrouiller un abonnement, le groupe de ressources ou la ressource tooprevent autres utilisateurs de votre organisation d’accidentellement supprimer ou modifier des ressources critiques. Pour plus d’informations, consultez [Verrouiller des ressources avec Azure Resource Manager](resource-group-lock-resources.md).

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a>Afficher votre abonnement et vos coûts
Vous pouvez afficher plus d’informations sur votre abonnement et les coûts de multi-niveaux hello pour toutes vos ressources. Sélectionnez **abonnements** et abonnement hello toosee. Vous pouvez uniquement avoir un abonnement tooselect.

![abonnement](./media/resource-group-portal/select-subscription.png)

Dans le panneau d’abonnement hello, vous voyez un taux d’avancement.

![taux d’avancement](./media/resource-group-portal/burn-rate.png)

Ainsi qu’une répartition des coûts par type de ressource.

![coût des ressources](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a>Exportation du modèle
Après avoir configuré votre groupe de ressources, vous pouvez choisir modèle de gestionnaire de ressources tooview hello pour le groupe de ressources hello. Exportation de modèle de hello offre deux avantages :

1. Vous pouvez automatiser facilement les futurs déploiements de solution de hello, car le modèle de hello contient une infrastructure complète hello tous les.
2. Vous pouvez vous familiariser avec la syntaxe de modèle en examinant hello Notation JSON (JavaScript Object) qui représente votre solution.

Pour obtenir des instructions détaillées, voir [Exporter un modèle Azure Resource Manager à partir de ressources existantes](resource-manager-export-template.md).

## <a name="delete-resource-group-or-resources"></a>Supprimer des ressources ou un groupe de ressources
Suppression d’un groupe de ressources supprime toutes les ressources hello qu’il contient. Vous pouvez également supprimer des ressources individuelles d'un groupe de ressources. Vous souhaitez tooexercise attention lorsque vous supprimez un groupe de ressources, car il peut y avoir des ressources dans d’autres groupes de ressources sont tooit lié. Le Gestionnaire de ressources ne supprime pas les ressources liées, mais ils ne peuvent pas fonctionner correctement sans les ressources hello attendu.

![supprimer un groupe](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a>Étapes suivantes
* journaux d’activité tooview, consultez [auditer les opérations effectuées avec le Gestionnaire de ressources](resource-group-audit.md).
* tooview plus d’informations sur le déploiement, consultez [afficher les opérations de déploiement](resource-manager-deployment-operations.md).
* ressources toodeploy via le portail de hello, consultez [déployer des ressources avec des modèles de gestionnaire de ressources et le portail Azure](resource-group-template-deploy-portal.md).
* toomanage accès tooresources, consultez [utiliser les ressources de rôle affectations toomanage accès tooyour abonnement Azure](../active-directory/role-based-access-control-configure.md).
* Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).

