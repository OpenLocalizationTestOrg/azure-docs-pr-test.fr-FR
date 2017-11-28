---
title: "Déployer des ressources sur Azure | Microsoft Docs"
description: "Utilisez Azure PowerShell ou l’interface de ligne de commande Azure pour déployer des ressources sur Azure. Les ressources sont définies dans un modèle Resource Manager."
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
ms.openlocfilehash: 19d5ec337a18b1a159de05ed611b2ccd0c15c592
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-resources-to-azure"></a><span data-ttu-id="daac2-104">Déployer des ressources sur Azure</span><span class="sxs-lookup"><span data-stu-id="daac2-104">Deploy resources to Azure</span></span>

<span data-ttu-id="daac2-105">Cette rubrique explique comment déployer des ressources sur votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="daac2-105">This topic shows how to deploy resources to your Azure subscription.</span></span> <span data-ttu-id="daac2-106">Vous pouvez utiliser Azure PowerShell ou l’interface de ligne de commande Azure pour déployer un modèle Resource Manager qui définit l’infrastructure de votre solution.</span><span class="sxs-lookup"><span data-stu-id="daac2-106">You can use either Azure PowerShell or Azure CLI to deploy a Resource Manager template that defines the infrastructure for your solution.</span></span>

<span data-ttu-id="daac2-107">Pour une introduction aux concepts de Resource Manager, consultez [Vue d'ensemble d’Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="daac2-107">For an introduction to concepts of Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="steps-for-deployment"></a><span data-ttu-id="daac2-108">Étapes de déploiement</span><span class="sxs-lookup"><span data-stu-id="daac2-108">Steps for deployment</span></span>

<span data-ttu-id="daac2-109">Cette rubrique suppose que vous déployez l[’exemple de modèle de stockage](#example-storage-template) dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="daac2-109">This topic assumes you are deploying the [example storage template](#example-storage-template) in this topic.</span></span> <span data-ttu-id="daac2-110">Vous pouvez utiliser un modèle différent, mais les paramètres que vous transmettez sont différents de ceux indiqués dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="daac2-110">You can use a different template, but the parameters you pass are different than what is shown in this topic.</span></span>

<span data-ttu-id="daac2-111">Après avoir créé un modèle, les étapes générales pour le déploiement de votre modèle sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="daac2-111">After creating a template, the general steps for deploying your template are:</span></span>

1. <span data-ttu-id="daac2-112">Se connecter à son compte</span><span class="sxs-lookup"><span data-stu-id="daac2-112">Log in to your account</span></span>
2. <span data-ttu-id="daac2-113">Sélectionnez l’abonnement à utiliser (uniquement si vous en avez plusieurs et souhaitez utiliser un abonnement qui n’est pas celui défini par défaut)</span><span class="sxs-lookup"><span data-stu-id="daac2-113">Select the subscription to use (only necessary if you have multiple subscriptions, and you want to use one that is not the default subscription)</span></span>
3. <span data-ttu-id="daac2-114">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="daac2-114">Create a resource group</span></span>
4. <span data-ttu-id="daac2-115">Déployer le modèle</span><span class="sxs-lookup"><span data-stu-id="daac2-115">Deploy the template</span></span>
5. <span data-ttu-id="daac2-116">Vérifier l’état de votre déploiement</span><span class="sxs-lookup"><span data-stu-id="daac2-116">Check your deployment status</span></span>

<span data-ttu-id="daac2-117">Les sections suivantes vous expliquent comment effectuer ces étapes à l’aide de [PowerShell](#powershell) ou de [l’interface de ligne de commande Azure](#azure-cli).</span><span class="sxs-lookup"><span data-stu-id="daac2-117">The following sections show how to perform those steps with [PowerShell](#powershell) or [Azure CLI](#azure-cli).</span></span>

## <a name="powershell"></a><span data-ttu-id="daac2-118">PowerShell</span><span class="sxs-lookup"><span data-stu-id="daac2-118">PowerShell</span></span>

1. <span data-ttu-id="daac2-119">Pour Installer Azure PowerShell, consultez [Prise en main des applets de commande Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="daac2-119">To install Azure PowerShell, see [Get started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>

2. <span data-ttu-id="daac2-120">Pour commencer le déploiement rapidement, utilisez les applets de commande suivantes :</span><span class="sxs-lookup"><span data-stu-id="daac2-120">To quickly get started with deployment, use the following cmdlets:</span></span>

  ```powershell
  Login-AzureRmAccount
  Set-AzureRmContext -SubscriptionID {subscription-id}

  New-AzureRmResourceGroup -Name ExampleGroup -Location "Central US"
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json 
  ```

  <span data-ttu-id="daac2-121">L’applet de commande `Set-AzureRmContext` est nécessaire uniquement si vous souhaitez utiliser un abonnement autre que votre abonnement par défaut.</span><span class="sxs-lookup"><span data-stu-id="daac2-121">The `Set-AzureRmContext` cmdlet is only needed if you want to use a subscription other than your default subscription.</span></span> <span data-ttu-id="daac2-122">Pour afficher tous vos abonnements et leurs numéros d’identification, utilisez :</span><span class="sxs-lookup"><span data-stu-id="daac2-122">To see all your subscriptions and their IDs, use:</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="daac2-123">Le déploiement peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="daac2-123">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="daac2-124">Une fois l’opération terminée, un message similaire à celui apparaît :</span><span class="sxs-lookup"><span data-stu-id="daac2-124">When it finishes, you see a message similar to:</span></span>

  ```powershell
  DeploymentName          : ExampleDeployment
  CorrelationId           : 07b3b233-8367-4a0b-b9bc-7aa189065665
  ResourceGroupName       : ExampleGroup
  ProvisioningState       : Succeeded
  ...
  ```

4. <span data-ttu-id="daac2-125">Pour vérifier que votre groupe de ressources et votre compte de stockage ont été déployés sur votre abonnement, utilisez :</span><span class="sxs-lookup"><span data-stu-id="daac2-125">To see that your resource group and storage account were deployed to your subscription, use:</span></span>

  ```powershell
  Get-AzureRmResourceGroup -Name ExampleGroup
  Find-AzureRmResource -ResourceGroupNameEquals ExampleGroup
  ```

5. <span data-ttu-id="daac2-126">Vous pouvez spécifier des modèles de paramètres comme paramètres PowerShell lors du déploiement d’un modèle.</span><span class="sxs-lookup"><span data-stu-id="daac2-126">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="daac2-127">Comme l’exemple précédent ne comportait aucun modèle de paramètre, les valeurs par défaut du modèle ont été utilisées.</span><span class="sxs-lookup"><span data-stu-id="daac2-127">The earlier example did not include any template parameters, so the default values in the template were used.</span></span> <span data-ttu-id="daac2-128">Pour déployer un autre compte de stockage et fournir des valeurs de paramètres pour le préfixe du nom de stockage et la référence du compte de stockage, utilisez :</span><span class="sxs-lookup"><span data-stu-id="daac2-128">To deploy another storage account, and provide parameter values for the storage name prefix and the storage account SKU, use:</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment2 -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json -storageNamePrefix "contoso" -storageSKU "Standard_GRS"
  ```

  <span data-ttu-id="daac2-129">Vous disposez maintenant de deux comptes de stockage dans votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="daac2-129">You now have two storage accounts in your resource group.</span></span> 

## <a name="azure-cli"></a><span data-ttu-id="daac2-130">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="daac2-130">Azure CLI</span></span>

1. <span data-ttu-id="daac2-131">Pour installer l’interface de ligne de commande Azure, consultez [Installer l’interface de ligne de commande Azure 2.0](/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="daac2-131">To install Azure CLI, see [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

2. <span data-ttu-id="daac2-132">Pour commencer le déploiement rapidement, utilisez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="daac2-132">To quickly get started with deployment, use the following commands:</span></span>

  ```azurecli
  az login
  az account set --subscription {subscription-id}

  az group create --name ExampleGroup --location "Central US"
  az group deployment create --name ExampleDeployment --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json
  ```

  <span data-ttu-id="daac2-133">La commande `az account set` est uniquement nécessaire si vous souhaitez utiliser un abonnement autre que votre abonnement par défaut.</span><span class="sxs-lookup"><span data-stu-id="daac2-133">The `az account set` command is only needed if you want to use a subscription other than your default subscription.</span></span> <span data-ttu-id="daac2-134">Pour afficher tous vos abonnements et leurs numéros d’identification, utilisez :</span><span class="sxs-lookup"><span data-stu-id="daac2-134">To see all your subscriptions and their IDs, use:</span></span>

  ```azurecli
  az account list
  ```

3. <span data-ttu-id="daac2-135">Le déploiement peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="daac2-135">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="daac2-136">Une fois l’opération terminée, un message similaire à celui apparaît :</span><span class="sxs-lookup"><span data-stu-id="daac2-136">When it finishes, you see a message similar to:</span></span>

  ```azurecli
  "provisioningState": "Succeeded",
  ```

4. <span data-ttu-id="daac2-137">Pour vérifier que votre groupe de ressources et votre compte de stockage ont été déployés sur votre abonnement, utilisez :</span><span class="sxs-lookup"><span data-stu-id="daac2-137">To see that your resource group and storage account were deployed to your subscription, use:</span></span>

  ```azurecli
  az group show --name ExampleGroup
  az resource list --resource-group ExampleGroup
  ```

5. <span data-ttu-id="daac2-138">Vous pouvez spécifier des modèles de paramètres comme paramètres PowerShell lors du déploiement d’un modèle.</span><span class="sxs-lookup"><span data-stu-id="daac2-138">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="daac2-139">Comme l’exemple précédent ne comportait aucun modèle de paramètre, les valeurs par défaut du modèle ont été utilisées.</span><span class="sxs-lookup"><span data-stu-id="daac2-139">The earlier example did not include any template parameters, so the default values in the template were used.</span></span> <span data-ttu-id="daac2-140">Pour déployer un autre compte de stockage et fournir des valeurs de paramètres pour le préfixe du nom de stockage et la référence du compte de stockage, utilisez :</span><span class="sxs-lookup"><span data-stu-id="daac2-140">To deploy another storage account, and provide parameter values for the storage name prefix and the storage account SKU, use:</span></span>

  ```azurecli
  az group deployment create --name ExampleDeployment2 --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
  ```

  <span data-ttu-id="daac2-141">Vous disposez maintenant de deux comptes de stockage dans votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="daac2-141">You now have two storage accounts in your resource group.</span></span> 

## <a name="example-storage-template"></a><span data-ttu-id="daac2-142">Exemple de modèle de stockage</span><span class="sxs-lookup"><span data-stu-id="daac2-142">Example storage template</span></span>

<span data-ttu-id="daac2-143">Utilisez l’exemple de modèle suivant pour déployer un compte de stockage sur votre abonnement :</span><span class="sxs-lookup"><span data-stu-id="daac2-143">Use the following example template to deploy a storage account to your subscription:</span></span>

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
        "description": "The value to use for starting the storage account name."
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
        "description": "The type of replication to use for the storage account."
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

## <a name="next-steps"></a><span data-ttu-id="daac2-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="daac2-144">Next steps</span></span>

* <span data-ttu-id="daac2-145">Pour plus d’informations sur l’utilisation de PowerShell afin de déployer des modèles, consultez [Déployer des ressources à l’aide de modèles Resource Manager et d’Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="daac2-145">For detailed information about using PowerShell to deploy templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).</span></span>
* <span data-ttu-id="daac2-146">Pour plus d’informations sur l’utilisation de l’interface de ligne de commande Azure afin de déployer des modèles, consultez [Déployer des ressources à l’aide de modèles Resource Manager et de l’interface de ligne de commande Azure](/azure/azure-resource-manager/resource-group-template-deploy-cli).</span><span class="sxs-lookup"><span data-stu-id="daac2-146">For detailed information about using Azure CLI to deploy templates, see [Deploy resources with Resource Manager templates and Azure CLI](/azure/azure-resource-manager/resource-group-template-deploy-cli).</span></span>



