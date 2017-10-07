---
title: "aaaDeploy ensemble d’échelle de Machine virtuelle à l’aide de Visual Studio | Documents Microsoft"
description: "Déployer des jeux de mise à l'échelle de machines virtuelles à l'aide de Visual Studio et d’un modèle Resource Manager"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed0786b8-34b2-49a8-85b5-2a628128ead6
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c89a9f2478ccc3d22989aea604a4273bcc46df82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-visual-studio"></a>Comment toocreate une échelle de l’ordinateur virtuel défini avec Visual Studio
Cet article vous explique comment toodeploy une échelle de machines virtuelles Azure définie à l’aide d’un déploiement de groupe de ressources Visual Studio.

[Machines virtuelles Azure identiques](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) est une toodeploy de ressources de calcul Azure et de gérer une collection de machines virtuelles similaires à l’échelle automatique et de l’équilibrage de charge. Vous pouvez configurer et déployer des groupes de machines virtuelles identiques à l’aide de [modèles Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates). Les modèles Azure Resource Manager peuvent être déployés à l’aide de l’interface de ligne de commande (CLI) Azure, de PowerShell, de REST et directement à partir de Visual Studio. Visual Studio fournit des exemples de modèles qui peuvent être déployés dans le cadre d’un projet de déploiement de groupe de ressources Azure.

Déploiements de groupe de ressources Azure sont un moyen toogroup et publient un ensemble de ressources Azure connexes dans une même opération de déploiement. Pour en savoir plus, consultez la rubrique [Création et déploiement de groupes de ressources Azure à l’aide de Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)

## <a name="pre-requisites"></a>Conditions préalables
tooget de déployer des machines virtuelles identiques dans Visual Studio, hello éléments suivants sont nécessaires :

* Visual Studio 2013 ou une version ultérieure
* Kit de développement logiciel (SDK) Azure 2.7, 2.8 ou 2.9

>[!NOTE]
>Ces instructions partent du principe que vous utilisez Visual Studio avec le [Kit de développement logiciel (SDK) Azure 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).

## <a name="creating-a-project"></a>Création d’un projet
1. Créez un projet dans Visual Studio en sélectionnant **Fichier | Nouveau | Projet**.
   
    ![Fichier Nouveau][file_new]

2. Sous **Visual C# | Cloud**, choisissez **Azure Resource Manager** toocreate un projet pour le déploiement d’un modèle de gestionnaire de ressources Azure.
   
    ![Créer un projet][create_project]

3. À partir de la liste de hello des modèles, sélectionnez hello Linux ou modèle de définir de mise à l’échelle d’ordinateur virtuel Windows.
   
   ![Sélectionner un modèle][select_Template]

4. Une fois votre projet créé, vous voyez les scripts de déploiement PowerShell, un modèle de gestionnaire de ressources Azure et un fichier de paramètres pour hello ensemble d’échelle de Machine virtuelle.
   
    ![Explorateur de solutions][solution_explorer]

## <a name="customize-your-project"></a>Personnalisation de votre projet
Maintenant vous pouvez modifier toocustomize du modèle hello pour les besoins de votre application, telles que l’ajout de propriétés d’extension de machine virtuelle ou la modification de charger les règles d’équilibrage. Par défaut les modèles d’ensembles hello Machine virtuelle mise à l’échelle sont extension toodeploy configuré hello AzureDiagnostics, ce qui rend les règles de mise à l’échelle tooadd facile. Il déploie également un équilibreur de charge avec une adresse IP publique, configuré avec les règles NAT entrantes. 

équilibrage de charge Hello vous permet de connecter des instances de machine virtuelle toohello avec SSH (Linux) ou RDP (Windows). plage de ports frontaux de Hello commence à 50000. Pour linux, cela signifie que si vous SSH tooport 50000, vous êtes routé tooport 22 de hello première machine virtuelle Bonjour ensemble d’échelle. Connexion tooport 50001 est routé tooport 22 Hello deuxième machine virtuelle et ainsi de suite.

 Un bon moyen tooedit vos modèles avec Visual Studio est le paramètres hello tooorganize toouse hello structure JSON, des variables et des ressources. Le fonctionnement de hello schéma Visual Studio peut souligner les erreurs dans votre modèle avant de le déployer.

![JSON Explorer][json_explorer]

## <a name="deploy-hello-project"></a>Déployer le projet de hello
1. Déployer hello Azure Resource Manager ressource modèle de toocreate hello ensemble d’échelle de Machine virtuelle. Avec le bouton droit sur le nœud de projet hello et choisissez **déployer | Nouveau déploiement**.
   
    ![Déployer un modèle][5deploy_Template]
    
2. Dans la boîte de dialogue « Déployer tooResource groupe » hello, sélectionnez votre abonnement.
   
    ![Déployer un modèle][6deploy_Template]

3. À ce stade, vous pouvez créer un groupe de ressources Azure de toodeploy votre modèle de.
   
    ![Nouveau groupe de ressources][new_resource]

4. Ensuite, cliquez sur **modifier les paramètres** tooenter les paramètres qui sont passés tooyour modèle. Fournissez hello username et password pour hello du système d’exploitation, qui est le déploiement de hello toocreate requis. Si vous n’avez outils PowerShell pour Visual Studio est installé, il est recommandé de toocheck **enregistrer les mots de passe** tooavoid une ligne de commande PowerShell masqué invite, ou utilisez [prise en charge keyvault](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).
   
    ![Modifier les paramètres][edit_parameters]

5. Cliquez maintenant sur **Déployer**. Hello **sortie** fenêtre affiche la progression du déploiement hello. Notez que les actions hello exécute hello **Deploy-azureresourcegroup.ps1** script.
   
   ![Fenêtre Sortie][output_window]

## <a name="exploring-your-virtual-machine-scale-set"></a>Exploration de votre groupe de machines virtuelles identiques
Hello déploiement terminé, vous pouvez afficher hello nouvelle Machine virtuelle ensemble d’échelle Bonjour Visual Studio **Cloud Explorer** (liste d’actualisation hello). Cloud Explorer vous permet de gérer des ressources Azure dans Visual Studio lors du développement d'applications. Vous pouvez également afficher votre ensemble d’échelle de Machine virtuelle dans hello [portail Azure](https://portal.azure.com) et [Explorateur de ressources Azure](https://resources.azure.com/).

![Cloud Explorer][cloud_explorer]

 portail de Hello fournit la meilleure hello toovisually gérer votre infrastructure d’Azure avec un navigateur web, alors que l’Explorateur de ressources Azure fournit un moyen simple de tooexplore et débogage des ressources Azure, ce qui dans une fenêtre de hello « afficher les instance » et en montrant également PowerShell commandes pour les ressources hello que vous examinez.

## <a name="next-steps"></a>Étapes suivantes
Une fois que vous avez correctement déployé des machines virtuelles identiques via Visual Studio, vous pouvez personnaliser davantage votre toosuit projet spécifications de votre application. Par exemple, configurer à l’échelle automatique en ajoutant un **Insights** ressource, ajout d’infrastructure tooyour modèle (comme les ordinateurs virtuels autonomes), ou du déploiement des applications à l’aide d’extension de script personnalisé hello. Bon exemple modèles se trouvent dans hello [modèles de démarrage rapide Azure](https://github.com/Azure/azure-quickstart-templates) le référentiel GitHub (recherche de « mise »).

[file_new]: ./media/virtual-machine-scale-sets-vs-create/1-FileNew.png
[create_project]: ./media/virtual-machine-scale-sets-vs-create/2-CreateProject.png
[select_Template]: ./media/virtual-machine-scale-sets-vs-create/3b-SelectTemplateLin.png
[solution_explorer]: ./media/virtual-machine-scale-sets-vs-create/4-SolutionExplorer.png
[json_explorer]: ./media/virtual-machine-scale-sets-vs-create/10-JsonExplorer.png
[5deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/5-DeployTemplate.png
[6deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/6-DeployTemplate.png
[new_resource]: ./media/virtual-machine-scale-sets-vs-create/7-NewResourceGroup.png
[edit_parameters]: ./media/virtual-machine-scale-sets-vs-create/8-EditParameter.png
[output_window]: ./media/virtual-machine-scale-sets-vs-create/9-Output.png
[cloud_explorer]: ./media/virtual-machine-scale-sets-vs-create/12-CloudExplorer.png
