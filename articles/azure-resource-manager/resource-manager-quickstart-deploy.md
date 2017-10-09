---
title: aaaDeploy ressources tooAzure | Documents Microsoft
description: "Utilisez tooAzure de ressources toodeploy Azure PowerShell ou CLI d’Azure. ressources de Hello sont définies dans un modèle de gestionnaire de ressources."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/16/2017
ms.author: tomfitz
ms.openlocfilehash: 0cd3f8ad45af1fb85c78899b56f6807d00b859f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-tooazure"></a><span data-ttu-id="51952-104">Déployer des ressources tooAzure</span><span class="sxs-lookup"><span data-stu-id="51952-104">Deploy resources tooAzure</span></span>

<span data-ttu-id="51952-105">Cette rubrique montre comment toodeploy ressources tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="51952-105">This topic shows how toodeploy resources tooyour Azure subscription.</span></span> <span data-ttu-id="51952-106">Vous pouvez utiliser Azure PowerShell ou CLI d’Azure toodeploy un modèle de gestionnaire de ressources qui définit l’infrastructure hello pour votre solution.</span><span class="sxs-lookup"><span data-stu-id="51952-106">You can use either Azure PowerShell or Azure CLI toodeploy a Resource Manager template that defines hello infrastructure for your solution.</span></span>

<span data-ttu-id="51952-107">Pour une introduction tooconcepts du Gestionnaire de ressources, consultez [vue d’ensemble du Gestionnaire de ressources Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="51952-107">For an introduction tooconcepts of Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="steps-for-deployment"></a><span data-ttu-id="51952-108">Étapes de déploiement</span><span class="sxs-lookup"><span data-stu-id="51952-108">Steps for deployment</span></span>

<span data-ttu-id="51952-109">Cette rubrique suppose que vous déployez hello [exemple de modèle de stockage](#example-storage-template) dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="51952-109">This topic assumes you are deploying hello [example storage template](#example-storage-template) in this topic.</span></span> <span data-ttu-id="51952-110">Vous pouvez utiliser un autre modèle, mais vous passez des paramètres de hello sont autre que celui indiqué dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="51952-110">You can use a different template, but hello parameters you pass are different than what is shown in this topic.</span></span>

<span data-ttu-id="51952-111">Après avoir créé un modèle, les étapes générales de hello pour le déploiement de votre modèle sont :</span><span class="sxs-lookup"><span data-stu-id="51952-111">After creating a template, hello general steps for deploying your template are:</span></span>

1. <span data-ttu-id="51952-112">Connectez-vous au compte de tooyour</span><span class="sxs-lookup"><span data-stu-id="51952-112">Log in tooyour account</span></span>
2. <span data-ttu-id="51952-113">Sélectionnez toouse d’abonnement hello (nécessaire uniquement si vous avez plusieurs abonnements et que vous souhaitez toouse qui n’est pas hello par défaut abonnement)</span><span class="sxs-lookup"><span data-stu-id="51952-113">Select hello subscription toouse (only necessary if you have multiple subscriptions, and you want toouse one that is not hello default subscription)</span></span>
3. <span data-ttu-id="51952-114">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="51952-114">Create a resource group</span></span>
4. <span data-ttu-id="51952-115">Déployer le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="51952-115">Deploy hello template</span></span>
5. <span data-ttu-id="51952-116">Vérifier l’état de votre déploiement</span><span class="sxs-lookup"><span data-stu-id="51952-116">Check your deployment status</span></span>

<span data-ttu-id="51952-117">Hello sections suivantes montrent comment tooperform ces étapes avec [PowerShell](#powershell) ou [CLI d’Azure](#azure-cli).</span><span class="sxs-lookup"><span data-stu-id="51952-117">hello following sections show how tooperform those steps with [PowerShell](#powershell) or [Azure CLI](#azure-cli).</span></span>

## <a name="powershell"></a><span data-ttu-id="51952-118">PowerShell</span><span class="sxs-lookup"><span data-stu-id="51952-118">PowerShell</span></span>

1. <span data-ttu-id="51952-119">tooinstall Azure PowerShell, consultez [prise en main des applets de commande Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="51952-119">tooinstall Azure PowerShell, see [Get started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>

2. <span data-ttu-id="51952-120">tooquickly prise en main déploiement, utilisez hello suivant d’applets de commande :</span><span class="sxs-lookup"><span data-stu-id="51952-120">tooquickly get started with deployment, use hello following cmdlets:</span></span>

  ```powershell
  Login-AzureRmAccount
  Set-AzureRmContext -SubscriptionID {subscription-id}

  New-AzureRmResourceGroup -Name ExampleGroup -Location "Central US"
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json 
  ```

  <span data-ttu-id="51952-121">Hello `Set-AzureRmContext` applet de commande est uniquement nécessaire si vous souhaitez toouse un abonnement autre que votre abonnement par défaut.</span><span class="sxs-lookup"><span data-stu-id="51952-121">hello `Set-AzureRmContext` cmdlet is only needed if you want toouse a subscription other than your default subscription.</span></span> <span data-ttu-id="51952-122">toosee tous vos abonnements et leurs ID, utilisez :</span><span class="sxs-lookup"><span data-stu-id="51952-122">toosee all your subscriptions and their IDs, use:</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="51952-123">déploiement de Hello peut prendre quelques minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="51952-123">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="51952-124">Une fois l’opération terminée, un message similaire à celui apparaît :</span><span class="sxs-lookup"><span data-stu-id="51952-124">When it finishes, you see a message similar to:</span></span>

  ```powershell
  DeploymentName          : ExampleDeployment
  CorrelationId           : 07b3b233-8367-4a0b-b9bc-7aa189065665
  ResourceGroupName       : ExampleGroup
  ProvisioningState       : Succeeded
  ...
  ```

4. <span data-ttu-id="51952-125">toosee votre compte de stockage et le groupe de ressources ont été déployés tooyour abonnement, utilisez :</span><span class="sxs-lookup"><span data-stu-id="51952-125">toosee that your resource group and storage account were deployed tooyour subscription, use:</span></span>

  ```powershell
  Get-AzureRmResourceGroup -Name ExampleGroup
  Find-AzureRmResource -ResourceGroupNameEquals ExampleGroup
  ```

5. <span data-ttu-id="51952-126">Vous pouvez spécifier des modèles de paramètres comme paramètres PowerShell lors du déploiement d’un modèle.</span><span class="sxs-lookup"><span data-stu-id="51952-126">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="51952-127">Hello exemple précédent n’incluait pas tous les paramètres de modèle, afin de valeurs par défaut de hello dans le modèle de hello ont été utilisés.</span><span class="sxs-lookup"><span data-stu-id="51952-127">hello earlier example did not include any template parameters, so hello default values in hello template were used.</span></span> <span data-ttu-id="51952-128">toodeploy stockage d’un autre compte et fournir des valeurs de paramètre pour le préfixe du nom de stockage hello et compte de stockage hello référence (SKU), utilisez :</span><span class="sxs-lookup"><span data-stu-id="51952-128">toodeploy another storage account, and provide parameter values for hello storage name prefix and hello storage account SKU, use:</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment2 -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json -storageNamePrefix "contoso" -storageSKU "Standard_GRS"
  ```

  <span data-ttu-id="51952-129">Vous disposez maintenant de deux comptes de stockage dans votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="51952-129">You now have two storage accounts in your resource group.</span></span> 

## <a name="azure-cli"></a><span data-ttu-id="51952-130">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="51952-130">Azure CLI</span></span>

1. <span data-ttu-id="51952-131">tooinstall CLI d’Azure, consultez [installer Azure CLI 2.0](/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="51952-131">tooinstall Azure CLI, see [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

2. <span data-ttu-id="51952-132">tooquickly prise en main déploiement, utilisez hello suivant les commandes :</span><span class="sxs-lookup"><span data-stu-id="51952-132">tooquickly get started with deployment, use hello following commands:</span></span>

  ```azurecli
  az login
  az account set --subscription {subscription-id}

  az group create --name ExampleGroup --location "Central US"
  az group deployment create --name ExampleDeployment --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json
  ```

  <span data-ttu-id="51952-133">Hello `az account set` commande est uniquement nécessaire si vous souhaitez toouse un abonnement autre que votre abonnement par défaut.</span><span class="sxs-lookup"><span data-stu-id="51952-133">hello `az account set` command is only needed if you want toouse a subscription other than your default subscription.</span></span> <span data-ttu-id="51952-134">toosee tous vos abonnements et leurs ID, utilisez :</span><span class="sxs-lookup"><span data-stu-id="51952-134">toosee all your subscriptions and their IDs, use:</span></span>

  ```azurecli
  az account list
  ```

3. <span data-ttu-id="51952-135">déploiement de Hello peut prendre quelques minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="51952-135">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="51952-136">Une fois l’opération terminée, un message similaire à celui apparaît :</span><span class="sxs-lookup"><span data-stu-id="51952-136">When it finishes, you see a message similar to:</span></span>

  ```azurecli
  "provisioningState": "Succeeded",
  ```

4. <span data-ttu-id="51952-137">toosee votre compte de stockage et le groupe de ressources ont été déployés tooyour abonnement, utilisez :</span><span class="sxs-lookup"><span data-stu-id="51952-137">toosee that your resource group and storage account were deployed tooyour subscription, use:</span></span>

  ```azurecli
  az group show --name ExampleGroup
  az resource list --resource-group ExampleGroup
  ```

5. <span data-ttu-id="51952-138">Vous pouvez spécifier des modèles de paramètres comme paramètres PowerShell lors du déploiement d’un modèle.</span><span class="sxs-lookup"><span data-stu-id="51952-138">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="51952-139">Hello exemple précédent n’incluait pas tous les paramètres de modèle, afin de valeurs par défaut de hello dans le modèle de hello ont été utilisés.</span><span class="sxs-lookup"><span data-stu-id="51952-139">hello earlier example did not include any template parameters, so hello default values in hello template were used.</span></span> <span data-ttu-id="51952-140">toodeploy stockage d’un autre compte et fournir des valeurs de paramètre pour le préfixe du nom de stockage hello et compte de stockage hello référence (SKU), utilisez :</span><span class="sxs-lookup"><span data-stu-id="51952-140">toodeploy another storage account, and provide parameter values for hello storage name prefix and hello storage account SKU, use:</span></span>

  ```azurecli
  az group deployment create --name ExampleDeployment2 --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
  ```

  <span data-ttu-id="51952-141">Vous disposez maintenant de deux comptes de stockage dans votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="51952-141">You now have two storage accounts in your resource group.</span></span> 

## <a name="example-storage-template"></a><span data-ttu-id="51952-142">Exemple de modèle de stockage</span><span class="sxs-lookup"><span data-stu-id="51952-142">Example storage template</span></span>

<span data-ttu-id="51952-143">Utilisez hello suivant exemple modèle toodeploy un abonnement de tooyour de compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="51952-143">Use hello following example template toodeploy a storage account tooyour subscription:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name."
      }
    },
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "hello type of replication toouse for hello storage account."
      }
    }
  },
  "variables": {
    "storageName": "[concat(parameters('storageNamePrefix'), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-05-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {  }
}
```

## <a name="next-steps"></a><span data-ttu-id="51952-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="51952-144">Next steps</span></span>

* <span data-ttu-id="51952-145">Pour plus d’informations sur l’utilisation de modèles de toodeploy PowerShell, consultez [déployer des ressources avec des modèles de gestionnaire de ressources et d’Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="51952-145">For detailed information about using PowerShell toodeploy templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).</span></span>
* <span data-ttu-id="51952-146">Pour plus d’informations sur l’utilisation de modèles de toodeploy CLI d’Azure, consultez [déployer des ressources avec des modèles de gestionnaire de ressources et CLI d’Azure](/azure/azure-resource-manager/resource-group-template-deploy-cli).</span><span class="sxs-lookup"><span data-stu-id="51952-146">For detailed information about using Azure CLI toodeploy templates, see [Deploy resources with Resource Manager templates and Azure CLI](/azure/azure-resource-manager/resource-group-template-deploy-cli).</span></span>



