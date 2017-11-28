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
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-cli"></a><span data-ttu-id="8ea41-103">Déployer un modèle Resource Manager privé avec un jeton SAP et Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8ea41-103">Deploy private Resource Manager template with SAS token and Azure CLI</span></span>

<span data-ttu-id="8ea41-104">Lorsque votre modèle se trouve dans un compte de stockage, vous pouvez restreindre le modèle de toohello access et fournir un jeton de signature (SAS) d’accès partagé au cours du déploiement.</span><span class="sxs-lookup"><span data-stu-id="8ea41-104">When your template resides in a storage account, you can restrict access toohello template and provide a shared access signature (SAS) token during deployment.</span></span> <span data-ttu-id="8ea41-105">Cette rubrique explique comment toouse Azure PowerShell avec le Gestionnaire de ressources modèles tooprovide un jeton SAP durant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="8ea41-105">This topic explains how toouse Azure PowerShell with Resource Manager templates tooprovide a SAS token during deployment.</span></span> 

## <a name="add-private-template-toostorage-account"></a><span data-ttu-id="8ea41-106">Ajouter le compte toostorage de modèle privé</span><span class="sxs-lookup"><span data-stu-id="8ea41-106">Add private template toostorage account</span></span>

<span data-ttu-id="8ea41-107">Vous pouvez ajouter votre compte de stockage de modèles tooa et la liaison de toothem pendant le déploiement avec un jeton SAP.</span><span class="sxs-lookup"><span data-stu-id="8ea41-107">You can add your templates tooa storage account and link toothem during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ea41-108">En suivant les étapes de hello ci-dessous, blob hello contenant le modèle de hello est propriétaire du compte hello tooonly accessible.</span><span class="sxs-lookup"><span data-stu-id="8ea41-108">By following hello steps below, hello blob containing hello template is accessible tooonly hello account owner.</span></span> <span data-ttu-id="8ea41-109">Toutefois, lorsque vous créez un jeton SAS pour l’objet blob de hello, objet blob de hello est tooanyone accessible avec cet URI.</span><span class="sxs-lookup"><span data-stu-id="8ea41-109">However, when you create a SAS token for hello blob, hello blob is accessible tooanyone with that URI.</span></span> <span data-ttu-id="8ea41-110">Si un autre utilisateur intercepte hello URI, cet utilisateur est modèle de hello en mesure de tooaccess.</span><span class="sxs-lookup"><span data-stu-id="8ea41-110">If another user intercepts hello URI, that user is able tooaccess hello template.</span></span> <span data-ttu-id="8ea41-111">À l’aide d’un jeton SAP est un bon moyen de limiter l’accès tooyour modèles, mais n’incluez pas les données sensibles telles que les mots de passe directement dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="8ea41-111">Using a SAS token is a good way of limiting access tooyour templates, but you should not include sensitive data like passwords directly in hello template.</span></span>
> 
> 

<span data-ttu-id="8ea41-112">Hello exemple suivant définit un conteneur du compte de stockage privé et télécharge un modèle :</span><span class="sxs-lookup"><span data-stu-id="8ea41-112">hello following example sets up a private storage account container and uploads a template:</span></span>
   
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

### <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="8ea41-113">Fournir un jeton SAP au cours du déploiement</span><span class="sxs-lookup"><span data-stu-id="8ea41-113">Provide SAS token during deployment</span></span>
<span data-ttu-id="8ea41-114">toodeploy un modèle privé dans un compte de stockage, générer un jeton SAP et incluez-le dans hello URI pour le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="8ea41-114">toodeploy a private template in a storage account, generate a SAS token and include it in hello URI for hello template.</span></span> <span data-ttu-id="8ea41-115">Définissez tooallow de temps d’expiration hello suffisamment déploiement toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="8ea41-115">Set hello expiry time tooallow enough time toocomplete hello deployment.</span></span>
   
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

<span data-ttu-id="8ea41-116">Pour accéder à un exemple d’utilisation d’un jeton SAP avec des modèles liés, consultez [Utilisation de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8ea41-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ea41-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8ea41-117">Next steps</span></span>
* <span data-ttu-id="8ea41-118">Pour une toodeploying des modèles de présentation, consultez [déployer des ressources avec des modèles de gestionnaire de ressources et d’Azure PowerShell](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8ea41-118">For an introduction toodeploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy-cli.md).</span></span>
* <span data-ttu-id="8ea41-119">Pour accéder à un exemple de script complet qui déploie un modèle, consultez la page [Azure Resource Manager template deployment - PowerShell script](resource-manager-samples-cli-deploy.md) (Déploiement d’un modèle Azure Resource Manager - Script PowerShell)</span><span class="sxs-lookup"><span data-stu-id="8ea41-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-cli-deploy.md)</span></span>
* <span data-ttu-id="8ea41-120">paramètres de toodefine dans le modèle, consultez [création de modèles](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="8ea41-120">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="8ea41-121">Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="8ea41-121">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
