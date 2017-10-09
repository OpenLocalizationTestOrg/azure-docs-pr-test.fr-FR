---
title: aaaUse toodeploy portail Azure ressources Azure | Documents Microsoft
description: "Utiliser le portail Azure et gérer les ressources Azure de toodeploy vos ressources."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 2c98a4aa-8d9f-4a0a-b764-214dbe8ed009
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 5a5217f94c8dfc0c1ebd613903ea3dcbe1197bfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a>Déployer des ressources à l’aide de modèles Resource Manager et du Portail Azure
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [Interface de ligne de commande Azure](resource-group-template-deploy-cli.md)
> * [Portail](resource-group-template-deploy-portal.md)
> * [API REST](resource-group-template-deploy-rest.md)
> 
> 

Cette rubrique montre comment toouse hello [portail Azure](https://portal.azure.com) avec [Azure Resource Manager](resource-group-overview.md) toodeploy vos ressources Azure. toolearn sur la gestion de vos ressources, consultez [des ressources de gestion de Azure via le portail](resource-group-portal.md).

Actuellement, pas tous les services prend en charge le portail de hello ou Gestionnaire de ressources. Pour ces services, vous devez toouse hello [portail classic](https://manage.windowsazure.com). Statut de hello de chaque service, consultez [graphique de la disponibilité de portail Azure](https://azure.microsoft.com/features/azure-portal/availability/).

## <a name="create-resource-group"></a>Créer un groupe de ressources
1. toocreate un groupe de ressources vide, sélectionnez **nouveau** > **gestion** > **groupe de ressources**.
   
    ![créer un groupe de ressources vide](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. Spécifiez un nom et un emplacement, puis, si nécessaire, sélectionnez un abonnement. Vous devez tooprovide un emplacement pour le groupe de ressources hello, car le groupe de ressources hello stocke les métadonnées sur les ressources de hello. Pour des raisons de compatibilité, vous souhaiterez toospecify où que les métadonnées sont stockées. En règle générale, nous vous recommandons de spécifier l’emplacement où réside la plupart de vos ressources. À l’aide de hello même emplacement peut simplifier votre modèle.
   
    ![définir les valeurs d’un groupe](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a>Déployer des ressources à partir de Marketplace
Après avoir créé un groupe de ressources, vous pouvez déployer tooit de ressources à partir de hello Marketplace. Hello Marketplace fournit des solutions prédéfinies pour les scénarios courants.

1. toostart un déploiement, sélectionnez **nouveau** et hello type de ressource, vous aimeriez toodeploy. Ensuite, recherchez version particulière de hello de ressource de hello vous aimeriez toodeploy.
   
    ![déployer des ressources](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. Si vous ne voyez pas de solution spécifique de hello toodeploy voulue, vous pouvez rechercher hello Marketplace.
   
    ![effectuer une recherche sur le marketplace](./media/resource-group-template-deploy-portal/search-resource.png)
3. En fonction de type hello de ressource sélectionnée, vous avez une collection de propriétés pertinentes des tooset avant le déploiement. Ces options ne sont pas présentées ici, car elles varient selon le type de ressource. Pour tous les types, vous devez sélectionner un groupe de ressources de destination. image de suivante de Hello montre comment toocreate une application web et le déployer le groupe de ressources toohello vous avez créé.
   
    ![Créer un groupe de ressources](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    Ou bien, vous pouvez décider toocreate un groupe de ressources lors du déploiement de vos ressources. Sélectionnez **nouvel** et donnez un nom à groupe de ressources hello.
   
    ![créer un groupe de ressources](./media/resource-group-template-deploy-portal/select-new-group.png)
4. Votre déploiement se met en route. déploiement de Hello peut prendre quelques minutes. Déploiement de hello terminée, vous voyez une notification.
   
    ![afficher une notification](./media/resource-group-template-deploy-portal/view-notification.png)
5. Après avoir déployé vos ressources, vous pouvez ajouter le groupe de ressources de plusieurs ressources toohello à l’aide de hello **ajouter** commande sur le panneau des ressources de groupe hello.
   
    ![ajouter une ressource](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a>Déployer des ressources à partir d’un modèle personnalisé
Si vous voulez tooexecute un déploiement mais pas un des modèles de hello Bonjour Marketplace, vous pouvez créer un modèle personnalisé qui définit l’infrastructure hello pour votre solution. toolearn sur la création de modèles, consultez [les modèles de programmation Azure Resource Manager](resource-group-authoring-templates.md).

1. toodeploy un modèle personnalisé via le portail de hello, sélectionnez **nouveau**et commencer à rechercher **déploiement d’un modèle** jusqu'à ce que vous pouvez le sélectionner à partir des options de hello.
   
    ![rechercher un déploiement de modèle](./media/resource-group-template-deploy-portal/search-template.png)
2. Sélectionnez **déploiement d’un modèle** à partir des ressources disponibles de hello.
   
    ![sélectionner un déploiement de modèle](./media/resource-group-template-deploy-portal/select-template.png)
3. Après le lancement du déploiement d’un modèle hello, ouvrez le modèle vide hello n’est disponible pour la personnalisation.
   
    ![créer un modèle](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    Dans l’éditeur de hello, ajoutez la syntaxe hello JSON qui définit les ressources hello toodeploy. Sélectionnez **Enregistrer** lorsque vous avez terminé. Pour obtenir des conseils sur l’écriture de syntaxe de hello JSON, consultez [procédure pas à pas de gestionnaire de ressources du modèle](resource-manager-template-walkthrough.md).
   
    ![modifier un modèle](./media/resource-group-template-deploy-portal/edit-template.png)
4. Ou bien, vous pouvez sélectionner un modèle existant à partir de hello [modèles de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates/). Ces modèles sont fournis par la Communauté de hello. Qu’ils couvrent de nombreux scénarios courants, et une personne a peut-être ajouté un modèle similaire toowhat vous essayez de toodeploy. Vous pouvez rechercher un élément qui correspond à votre scénario hello modèles toofind.
   
    ![sélectionner un modèle de démarrage rapide](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    Vous pouvez afficher le modèle sélectionné de hello dans l’éditeur de hello.
5. Après avoir entré hello toutes les autres valeurs, sélectionnez **créer** modèle de hello toodeploy. 
   
    ![déployer un modèle](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-tooyour-account"></a>Déployer des ressources à partir d’un modèle enregistré tooyour compte
Hello portail permet de toosave un tooyour modèle compte Azure et recommencer ultérieurement. Pour plus d’informations sur l’utilisation de ces enregistré des modèles, [prise en main des modèles privés sur hello portail Azure](../marketplace-consumer/mytemplates-getstarted.md).

1. sélectionner de vos modèles enregistrés, toofind **Parcourir** > **modèles**.
   
    ![parcourir les modèles](./media/resource-group-template-deploy-portal/browse-templates.png)
2. Dans liste de hello des modèles enregistrés tooyour compte, sélectionnez hello celui que vous souhaitez toowork sur.
   
    ![modèles enregistrés](./media/resource-group-template-deploy-portal/saved-templates.png)
3. Sélectionnez **déployer** tooredeploy que cela enregistré le modèle.
   
    ![déployer un modèle enregistré](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a>Étapes suivantes
* les journaux d’audit de tooview, consultez [auditer les opérations effectuées avec le Gestionnaire de ressources](resource-group-audit.md).
* tootroubleshoot des erreurs de déploiement, consultez [afficher les opérations de déploiement](resource-manager-deployment-operations.md).
* tooretrieve un modèle à partir d’un déploiement ou d’un groupe de ressources, consultez [modèle exporter Azure Resource Manager à partir de ressources existants](resource-manager-export-template.md).
* Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).

