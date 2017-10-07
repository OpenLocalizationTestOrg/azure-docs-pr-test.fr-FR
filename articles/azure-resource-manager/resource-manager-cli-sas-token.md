---
title: "aaaDeploy modèle Azure avec un jeton SAS et CLI d’Azure | Documents Microsoft"
description: "Utilisez tooAzure de ressources toodeploy Azure Resource Manager et CLI d’Azure à partir d’un modèle qui est protégé avec le jeton SAP."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: 59c64616d6e1f5e456d88a72854d0ed99e1bdc0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-cli"></a>Déployer un modèle Resource Manager privé avec un jeton SAP et Azure CLI

Lorsque votre modèle se trouve dans un compte de stockage, vous pouvez restreindre le modèle de toohello access et fournir un jeton de signature (SAS) d’accès partagé au cours du déploiement. Cette rubrique explique comment toouse Azure PowerShell avec le Gestionnaire de ressources modèles tooprovide un jeton SAP durant le déploiement. 

## <a name="add-private-template-toostorage-account"></a>Ajouter le compte toostorage de modèle privé

Vous pouvez ajouter votre compte de stockage de modèles tooa et la liaison de toothem pendant le déploiement avec un jeton SAP.

> [!IMPORTANT]
> En suivant les étapes de hello ci-dessous, blob hello contenant le modèle de hello est propriétaire du compte hello tooonly accessible. Toutefois, lorsque vous créez un jeton SAS pour l’objet blob de hello, objet blob de hello est tooanyone accessible avec cet URI. Si un autre utilisateur intercepte hello URI, cet utilisateur est modèle de hello en mesure de tooaccess. À l’aide d’un jeton SAP est un bon moyen de limiter l’accès tooyour modèles, mais n’incluez pas les données sensibles telles que les mots de passe directement dans le modèle de hello.
> 
> 

Hello exemple suivant définit un conteneur du compte de stockage privé et télécharge un modèle :
   
```azurecli
az group create --name "ManageGroup" --location "South Central US"
az storage account create \
    --resource-group ManageGroup \
    --location "South Central US" \
    --sku Standard_LRS \
    --kind Storage \
    --name {your-unique-name}
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
az storage container create \
    --name templates \
    --public-access Off \
    --connection-string $connection
az storage blob upload \
    --container-name templates \
    --file vmlinux.json \
    --name vmlinux.json \
    --connection-string $connection
```

### <a name="provide-sas-token-during-deployment"></a>Fournir un jeton SAP au cours du déploiement
toodeploy un modèle privé dans un compte de stockage, générer un jeton SAP et incluez-le dans hello URI pour le modèle de hello. Définissez tooallow de temps d’expiration hello suffisamment déploiement toocomplete hello.
   
```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
token=$(az storage blob generate-sas \
    --container-name templates \
    --name vmlinux.json \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name vmlinux.json \
    --output tsv \
    --connection-string $connection)
az group deployment create --resource-group ExampleGroup --template-uri $url?$token
```

Pour accéder à un exemple d’utilisation d’un jeton SAP avec des modèles liés, consultez [Utilisation de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).

## <a name="next-steps"></a>Étapes suivantes
* Pour une toodeploying des modèles de présentation, consultez [déployer des ressources avec des modèles de gestionnaire de ressources et d’Azure PowerShell](resource-group-template-deploy-cli.md).
* Pour accéder à un exemple de script complet qui déploie un modèle, consultez la page [Azure Resource Manager template deployment - PowerShell script](resource-manager-samples-cli-deploy.md) (Déploiement d’un modèle Azure Resource Manager - Script PowerShell)
* paramètres de toodefine dans le modèle, consultez [création de modèles](resource-group-authoring-templates.md#parameters).
* Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).
