---
title: "Déployer un modèle Azure avec le jeton SAP et l’interface Azure CLI | Microsoft Docs"
description: "Utilisez Azure Resource Manager et Azure CLI pour déployer des ressources dans Azure à partir d’un modèle protégé par un jeton SAP."
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
ms.openlocfilehash: 22387aadd8f53a65efb76a29a9403c46a2c25954
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-cli"></a><span data-ttu-id="98c77-103">Déployer un modèle Resource Manager privé avec un jeton SAP et Azure CLI</span><span class="sxs-lookup"><span data-stu-id="98c77-103">Deploy private Resource Manager template with SAS token and Azure CLI</span></span>

<span data-ttu-id="98c77-104">Lorsque votre modèle se trouve dans un compte de stockage, vous pouvez restreindre l’accès au modèle et fournir un jeton de signature d’accès partagé (SAP) au cours du déploiement.</span><span class="sxs-lookup"><span data-stu-id="98c77-104">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span></span> <span data-ttu-id="98c77-105">Cette rubrique explique comment utiliser Azure PowerShell avec les modèles Resource Manager pour fournir un jeton SAP lors du déploiement.</span><span class="sxs-lookup"><span data-stu-id="98c77-105">This topic explains how to use Azure PowerShell with Resource Manager templates to provide a SAS token during deployment.</span></span> 

## <a name="add-private-template-to-storage-account"></a><span data-ttu-id="98c77-106">Ajouter un modèle privé au compte de stockage</span><span class="sxs-lookup"><span data-stu-id="98c77-106">Add private template to storage account</span></span>

<span data-ttu-id="98c77-107">Vous pouvez ajouter vos modèles à un compte de stockage et les lier au cours du déploiement avec un jeton SAP.</span><span class="sxs-lookup"><span data-stu-id="98c77-107">You can add your templates to a storage account and link to them during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="98c77-108">Une fois les étapes ci-dessous suivies, l’objet blob contenant le modèle n’est accessible qu’au propriétaire du compte.</span><span class="sxs-lookup"><span data-stu-id="98c77-108">By following the steps below, the blob containing the template is accessible to only the account owner.</span></span> <span data-ttu-id="98c77-109">Toutefois, lorsque vous créez un jeton SAP pour l’objet blob, celui-ci est accessible à toute personne ayant cet URI.</span><span class="sxs-lookup"><span data-stu-id="98c77-109">However, when you create a SAS token for the blob, the blob is accessible to anyone with that URI.</span></span> <span data-ttu-id="98c77-110">Si un autre utilisateur intercepte l’URI, il pourra accéder au modèle.</span><span class="sxs-lookup"><span data-stu-id="98c77-110">If another user intercepts the URI, that user is able to access the template.</span></span> <span data-ttu-id="98c77-111">L’utilisation d’un jeton SAP est un bon moyen de limiter l’accès à vos modèles, mais vous ne devez pas inclure de données sensibles comme des mots de passe directement dans le modèle.</span><span class="sxs-lookup"><span data-stu-id="98c77-111">Using a SAS token is a good way of limiting access to your templates, but you should not include sensitive data like passwords directly in the template.</span></span>
> 
> 

<span data-ttu-id="98c77-112">L’exemple suivant configure un conteneur de compte de stockage privé et charge un modèle :</span><span class="sxs-lookup"><span data-stu-id="98c77-112">The following example sets up a private storage account container and uploads a template:</span></span>
   
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

### <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="98c77-113">Fournir un jeton SAP au cours du déploiement</span><span class="sxs-lookup"><span data-stu-id="98c77-113">Provide SAS token during deployment</span></span>
<span data-ttu-id="98c77-114">Pour déployer un modèle dans un compte de stockage privé, générez un jeton SAP et incluez-le dans l’URI du modèle.</span><span class="sxs-lookup"><span data-stu-id="98c77-114">To deploy a private template in a storage account, generate a SAS token and include it in the URI for the template.</span></span> <span data-ttu-id="98c77-115">Définissez le délai d’expiration de façon à laisser suffisamment de temps pour terminer le déploiement.</span><span class="sxs-lookup"><span data-stu-id="98c77-115">Set the expiry time to allow enough time to complete the deployment.</span></span>
   
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

<span data-ttu-id="98c77-116">Pour accéder à un exemple d’utilisation d’un jeton SAP avec des modèles liés, consultez [Utilisation de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="98c77-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="98c77-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="98c77-117">Next steps</span></span>
* <span data-ttu-id="98c77-118">Pour une introduction au déploiement de modèles, voir [Déployer des ressources à l’aide de modèles Resource Manager et d’Azure PowerShell](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="98c77-118">For an introduction to deploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy-cli.md).</span></span>
* <span data-ttu-id="98c77-119">Pour accéder à un exemple de script complet qui déploie un modèle, consultez la page [Azure Resource Manager template deployment - PowerShell script](resource-manager-samples-cli-deploy.md) (Déploiement d’un modèle Azure Resource Manager - Script PowerShell)</span><span class="sxs-lookup"><span data-stu-id="98c77-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-cli-deploy.md)</span></span>
* <span data-ttu-id="98c77-120">Pour définir des paramètres dans le modèle, consultez [Création de modèles](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="98c77-120">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="98c77-121">Pour obtenir des conseils sur l’utilisation de Resource Manager par les entreprises pour gérer efficacement les abonnements, voir [Structure d’Azure Enterprise - Gouvernance normative de l’abonnement](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="98c77-121">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
