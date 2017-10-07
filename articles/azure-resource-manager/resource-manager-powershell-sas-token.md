---
title: "aaaDeploy modèle Azure avec un jeton SAS et PowerShell | Documents Microsoft"
description: "Utiliser le Gestionnaire de ressources Azure et d’Azure PowerShell tooAzure de ressources toodeploy à partir d’un modèle qui est protégé avec jeton SAP."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: b95e096591d6213f8ef79235c8cd85705c4b79ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-powershell"></a>Déployer un modèle Resource Manager privé avec un jeton SAP et Azure PowerShell

Lorsque votre modèle se trouve dans un compte de stockage, vous pouvez restreindre le modèle de toohello access et fournir un jeton de signature (SAS) d’accès partagé au cours du déploiement. Cette rubrique explique comment toouse Azure PowerShell avec le Gestionnaire de ressources modèles tooprovide un jeton SAP durant le déploiement. 

## <a name="add-private-template-toostorage-account"></a>Ajouter le compte toostorage de modèle privé

Vous pouvez ajouter votre compte de stockage de modèles tooa et la liaison de toothem pendant le déploiement avec un jeton SAP.

> [!IMPORTANT]
> En suivant les étapes de hello ci-dessous, blob hello contenant le modèle de hello est propriétaire du compte hello tooonly accessible. Toutefois, lorsque vous créez un jeton SAS pour l’objet blob de hello, objet blob de hello est tooanyone accessible avec cet URI. Si un autre utilisateur intercepte hello URI, cet utilisateur est modèle de hello en mesure de tooaccess. À l’aide d’un jeton SAP est un bon moyen de limiter l’accès tooyour modèles, mais n’incluez pas les données sensibles telles que les mots de passe directement dans le modèle de hello.
> 
> 

Hello exemple suivant définit un conteneur du compte de stockage privé et télécharge un modèle :
   
```powershell
# create a storage account for templates
New-AzureRmResourceGroup -Name ManageGroup -Location "South Central US"
New-AzureRmStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name} -Type Standard_LRS -Location "West US"
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# create a container and upload template
New-AzureStorageContainer -Name templates -Permission Off
Set-AzureStorageBlobContent -Container templates -File c:\MyTemplates\storage.json
```

## <a name="provide-sas-token-during-deployment"></a>Fournir un jeton SAP au cours du déploiement
toodeploy un modèle privé dans un compte de stockage, générer un jeton SAP et incluez-le dans hello URI pour le modèle de hello. Définissez tooallow de temps d’expiration hello suffisamment déploiement toocomplete hello.
   
```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# get hello URI with hello SAS token
$templateuri = New-AzureStorageBlobSASToken -Container templates -Blob storage.json -Permission r `
  -ExpiryTime (Get-Date).AddHours(2.0) -FullUri

# provide URI with SAS token during deployment
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri $templateuri
```

Pour accéder à un exemple d’utilisation d’un jeton SAP avec des modèles liés, consultez [Utilisation de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).


## <a name="next-steps"></a>Étapes suivantes
* Pour une toodeploying des modèles de présentation, consultez [déployer des ressources avec des modèles de gestionnaire de ressources et d’Azure PowerShell](resource-group-template-deploy.md).
* Pour accéder à un exemple de script complet qui déploie un modèle, consultez la page [Azure Resource Manager template deployment - PowerShell script](resource-manager-samples-powershell-deploy.md) (Déploiement d’un modèle Azure Resource Manager - Script PowerShell)
* paramètres de toodefine dans le modèle, consultez [création de modèles](resource-group-authoring-templates.md#parameters).
* Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).

