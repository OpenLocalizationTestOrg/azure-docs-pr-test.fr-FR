---
title: "aaaCreate ou modifier des laboratoires automatiquement à l’aide de modèles Azure Resource Manager avec PowerShell | Documents Microsoft"
description: "Découvrez comment toouse les modèles Azure Resource Manager avec PowerShell toocreate ou modifier des laboratoires automatiquement dans un laboratoire DevTest"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: dad9944c-0b20-48be-ba80-8f4aa0950903
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: tarcher
ms.openlocfilehash: 29c8bc67caaec17b1f8926dde4e5d9d314b06600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-modify-labs-automatically-using-azure-resource-manager-templates-and-powershell"></a>Créer ou modifier des laboratoires automatiquement à l’aide de modèles Azure Resource Manager et PowerShell

DevTest Labs fournit de nombreux modèles Azure Resource Manager et scripts PowerShell qui peuvent vous aider à créer rapidement et automatiquement de nouveaux laboratoires ou à modifier des laboratoires existants, puis à déployer ces ressources.

Cet article vous aide à vous guider tout au long des processus de hello de l’utilisation de ces modèles et scripts tooautomate hello la création, modification et le déploiement de votre labs. Cet article vous indique également où vous trouverez plus d’informations sur comment toouse PowerShell tooperform courantes tâches DevTest Labs.

## <a name="step-1-gather-your-templates-and-scripts"></a>Étape 1 : rassembler vos modèles et scripts
Vous pouvez prédéfinir des [modèles Azure Resource Manager](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) et [scripts PowerShell](https://github.com/Azure/azure-devtestlab/tree/master/Scripts) dans notre [référentiel Github](https://github.com/Azure/azure-devtestlab) public. Utilisez-les tels quels ou adaptez-les à vos besoins et stockez-les dans votre propre [référentiel Git privé](devtest-lab-add-artifact-repo.md). 

## <a name="step-2-modify-your-azure-resource-manager-template"></a>Étape 2 : modifier votre modèle Azure Resource Manager
Vous pouvez suivre les étapes de hello à [créer votre premier modèle Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template) si vous n’avez jamais créé un modèle avant.

En outre, [meilleures pratiques pour la création de modèles Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) offre de nombreux toohelp d’instructions et des suggestions vous créez des modèles Azure Resource Manager sont toouse simple et fiable. En règle générale, vous allez utiliser une variation d’une des approches de hello ou exemples fournis et modifier votre modèle à vos besoins.

## <a name="step-3-deploy-resources-with-powershell"></a>Étape 3 : déployer des ressources avec PowerShell
Une fois que vous avez personnalisé vos modèles et les scripts, suivez les étapes hello nécessaires trop[déployer des ressources avec des modèles de gestionnaire de ressources et d’Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy). article de Hello fournit des informations générales sur l’utilisation d’Azure PowerShell avec Azure Resource Manager modèles toodeploy tooAzure de vos ressources.


## <a name="common-tasks-you-can-perform-in-devtest-labs-using-powershell"></a>Tâches courantes que vous pouvez effectuer dans DevTest Labs à l’aide de PowerShell
Il existe de nombreuses autres tâches courantes que vous pouvez automatiser à l’aide de PowerShell. Hello les sections suivantes de la documentation de hello montrer tooperform requis des étapes de hello ces tâches.

* [Créer une image personnalisée à partir d’un fichier de disque dur virtuel à l’aide de PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
* [Télécharger le compte de stockage de toolab du fichier de disque dur virtuel à l’aide de PowerShell](devtest-lab-upload-vhd-using-powershell.md)
* [Ajouter un laboratoire de tooa utilisateur externe à l’aide de PowerShell](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell)
* [Créer un rôle personnalisé de laboratoire à l’aide de PowerShell](devtest-lab-grant-user-permissions-to-specific-lab-policies.md#creating-a-lab-custom-role-using-powershell)

### <a name="next-steps"></a>Étapes suivantes
* Découvrez comment toocreate un [dépôt Git privé](devtest-lab-add-artifact-repo.md) où vous stockerez vos modèles personnalisés ou des scripts.
* Explorer hello [modèles Azure Resource Manager à partir de la galerie de modèles de démarrage rapide d’Azure](https://github.com/Azure/azure-quickstart-templates).
