---
title: "aaaView et utiliser Azure Resource Manager modèle une machine virtuelle | Documents Microsoft"
description: "Découvrez comment toouse hello modèle Azure Resource Manager à partir d’un ordinateur virtuel de toocreate autres machines virtuelles"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a759d9ce-655c-4ac6-8834-cb29dd7d30dd
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: tarcher
ms.openlocfilehash: b79f7eb4171793681a0b654e6e72a83191c76bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-virtual-machines-azure-resource-manager-template"></a>Utiliser un modèle Azure Resource Manager de machine virtuelle

Lorsque vous créez un ordinateur virtuel (VM) dans DevTest Labs via hello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), vous pouvez afficher le modèle de gestionnaire de ressources Azure hello avant de vous enregistrez hello machine virtuelle. Hello modèle peut ensuite être utilisé comme un toocreate base plus ordinateurs virtuels du laboratoire avec hello les mêmes paramètres.

Cet article décrit comment tooview hello modèle du Gestionnaire de ressources lors de la création d’une machine virtuelle et comment toodeploy il ultérieure tooautomate la création de hello même machine virtuelle.

## <a name="multi-vm-vs-single-vm-resource-manager-templates"></a>Modèles Resource Manager à plusieurs machines virtuelles ou à machine virtuelle unique
Il existe deux façons toocreate VM dans DevTest Labs, à l’aide d’un modèle de gestionnaire de ressources : configurer hello Microsoft.DevTestLab/labs/virtualmachines ressources ou configurer hello Microsoft.Commpute/virtualmachines ressources. Chaque méthode est utilisée dans des scénarios différents et nécessite des autorisations différentes.

- Modèles de gestionnaire de ressources qui utilisent un type de ressource Microsoft.DevTestLab/labs/virtualmachines (tel qu’il est déclaré dans la propriété de « ressource » hello dans le modèle de hello) peuvent configurer des ordinateurs virtuels de lab individuels. Chaque ordinateur virtuel puis affiche sous la forme d’un seul élément dans la liste d’ordinateurs virtuels DevTest Labs hello :

   ![Liste des ordinateurs virtuels en tant qu’éléments uniques dans la liste d’ordinateurs virtuels hello DevTest Labs](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-item.png)

   Ce type de modèle de gestionnaire de ressources peut être configuré par hello commande Azure PowerShell **New-AzureRmResourceGroupDeployment** ou via la commande CLI d’Azure de hello **créer de déploiement de groupe az** . Il requiert des autorisations d’administrateur, afin des utilisateurs assignés à un rôle d’utilisateur DevTest Labs ne peut pas effectuer le déploiement de hello. 

- Modèles de gestionnaire de ressources qui utilisent un type de ressource Microsoft.Compute/virtualmachines peuvent configurer plusieurs machines virtuelles en tant qu’un seul environnement dans la liste d’ordinateurs virtuels DevTest Labs hello :

   ![Liste des ordinateurs virtuels en tant qu’éléments uniques dans la liste d’ordinateurs virtuels hello DevTest Labs](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-environment.png)

   Machines virtuelles dans hello même environnement permettre être géré ensemble et partage hello même cycle de vie. Les utilisateurs sont affectés à un rôle d’utilisateur DevTest Labs peuvent créer des environnements à l’aide de ces modèles tant qu’administrateur de hello a configurés lab de hello de cette façon.

Hello reste de cet article présente les modèles de gestionnaire de ressources qui utilisent Mirosoft.DevTestLab/labs/virtualmachines. Ils sont utilisés par la création d’ordinateurs virtuels lab lab administrateurs tooautomate (par exemple, qui peuvent être réclamés VMs) ou génération de l’image finale (par exemple, en usine image).

[Meilleures pratiques pour la création de modèles Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) offre de nombreux toohelp d’instructions et des suggestions vous créez des modèles Azure Resource Manager sont toouse simple et fiable.

## <a name="view-and-save-a-virtual-machines-resource-manager-template"></a>Afficher et enregistrer un modèle Resource Manager de machine virtuelle
1. Suivez les étapes de hello à [créer votre première machine virtuelle dans un laboratoire](devtest-lab-create-first-vm.md) toobegin création d’un ordinateur virtuel.
1. Entrez les informations de hello requis pour votre machine virtuelle et ajouter les artefacts que vous souhaitez pour cette machine virtuelle.
1. En bas de hello de fenêtre de paramètres de configuration hello, choisissez **modèle vue ARM**.

   ![Bouton Afficher le modèle ARM](./media/devtest-lab-use-arm-template/devtestlab-lab-view-rm-template.png)
1. Copiez et enregistrez toouse de modèle de gestionnaire de ressources hello ultérieure toocreate une autre machine virtuelle.

   ![Toosave de modèle de gestionnaire de ressources pour une utilisation ultérieure](./media/devtest-lab-use-arm-template/devtestlab-lab-copy-rm-template.png)

Une fois que vous avez enregistré le modèle de gestionnaire de ressources hello, vous devez mettre à jour section des paramètres de modèle de hello hello avant que vous puissiez l’utiliser. Vous pouvez créer un parameter.json qui personnalise simplement les paramètres de hello, en dehors du modèle de gestionnaire de ressources réelle hello. 

![Personnaliser les paramètres à l’aide d’un fichier JSON](./media/devtest-lab-use-arm-template/devtestlab-lab-custom-params.png)

## <a name="deploy-a-resource-manager-template-toocreate-a-vm"></a>Déployer un toocreate de modèle de gestionnaire de ressources une machine virtuelle
Une fois que vous avez enregistré un modèle de gestionnaire de ressources et il adaptés à vos besoins, vous pouvez l’utiliser tooautomate création d’ordinateurs virtuels. [Déployer des ressources avec des modèles de gestionnaire de ressources et d’Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy) décrit comment toouse Azure PowerShell avec le Gestionnaire de ressources modèles toodeploy tooAzure de vos ressources. [Déployer des ressources avec des modèles de gestionnaire de ressources et CLI d’Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy-cli) décrit comment toouse CLI d’Azure avec le Gestionnaire de ressources modèles toodeploy tooAzure de vos ressources.

> [!NOTE]
> Seul un utilisateur disposant des autorisations de propriétaire de laboratoire peut créer des machines virtuelles à partir d’un modèle Resource Manager avec Azure PowerShell. Si vous voulez tooautomate la création d’ordinateurs virtuels à l’aide d’un modèle de gestionnaire de ressources et si vous disposez uniquement d’autorisations utilisateur, vous pouvez utiliser hello [ **créer des ordinateurs virtuels de lab az** commande hello CLI](https://docs.microsoft.com/cli/azure/lab/vm#create).

### <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[créer des environnements de multi-VM avec des modèles de gestionnaire de ressources](devtest-lab-create-environment-from-arm.md).
* Explorer les autres modèles de gestionnaire de ressources de démarrage rapide pour l’automatisation de DevTest Labs de hello [public DevTest Labs GitHub référentiel](https://github.com/Azure/azure-quickstart-templates).
