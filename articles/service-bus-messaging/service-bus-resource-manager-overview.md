---
title: "Création de ressources Azure Service Bus à l’aide de modèles Azure Resource Manager | Microsoft Docs"
description: "Utilisez les modèles Azure Resource Manager pour automatiser la création de ressources Service Bus"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 24f6a207-0fa4-49cf-8a58-963f9e2fd655
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: c8142d8edfd3a527b13d655bac21acf5332f2d14
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a><span data-ttu-id="f5d06-103">Création de ressources Service Bus à l’aide de modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f5d06-103">Create Service Bus resources using Azure Resource Manager templates</span></span>

<span data-ttu-id="f5d06-104">Cet article décrit comment créer et déployer des ressources Service Bus à l'aide de modèles Azure Resource Manager, de PowerShell et du fournisseur de ressources Service Bus.</span><span class="sxs-lookup"><span data-stu-id="f5d06-104">This article describes how to create and deploy Service Bus resources using Azure Resource Manager templates, PowerShell, and the Service Bus resource provider.</span></span>

<span data-ttu-id="f5d06-105">Les modèles Azure Resource Manager vous permettent de définir les ressources à déployer pour une solution et de spécifier les paramètres et variables qui permettent d'entrer des valeurs pour les différents environnements.</span><span class="sxs-lookup"><span data-stu-id="f5d06-105">Azure Resource Manager templates help you define the resources to deploy for a solution, and to specify parameters and variables that enable you to input values for different environments.</span></span> <span data-ttu-id="f5d06-106">Le modèle se compose d’un JSON et d’expressions que vous pouvez utiliser pour construire des valeurs pour votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="f5d06-106">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="f5d06-107">Pour plus d’informations sur l’écriture de modèles Azure Resource Manager et sur le format du modèle, consultez [Structure et syntaxe de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f5d06-107">For detailed information about writing Azure Resource Manager templates, and a discussion of the template format, see [structure and syntax of Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f5d06-108">Les exemples de cet article montrent comment utiliser Azure Resource Manager pour créer un espace de noms et une entité de messagerie (file d'attente) Service Bus.</span><span class="sxs-lookup"><span data-stu-id="f5d06-108">The examples in this article show how to use Azure Resource Manager to create a Service Bus namespace and messaging entity (queue).</span></span> <span data-ttu-id="f5d06-109">Pour accéder à d’autres exemples de modèles, recherchez « Service Bus » dans la [Galerie de modèles de démarrage rapide Azure][Azure Quickstart Templates gallery].</span><span class="sxs-lookup"><span data-stu-id="f5d06-109">For other template examples, visit the [Azure Quickstart Templates gallery][Azure Quickstart Templates gallery] and search for "Service Bus."</span></span>
>
>

## <a name="service-bus-resource-manager-templates"></a><span data-ttu-id="f5d06-110">Modèles Resource Manager Service Bus</span><span class="sxs-lookup"><span data-stu-id="f5d06-110">Service Bus Resource Manager templates</span></span>

<span data-ttu-id="f5d06-111">Ces modèles Azure Resource Manager Service Bus sont disponibles au téléchargement et au déploiement.</span><span class="sxs-lookup"><span data-stu-id="f5d06-111">These Service Bus Azure Resource Manager templates are available for download and deployment.</span></span> <span data-ttu-id="f5d06-112">Cliquez sur les liens suivants pour plus d'informations sur chacun d’eux, ainsi que des liens vers les modèles sur GitHub :</span><span class="sxs-lookup"><span data-stu-id="f5d06-112">Click the following links for details about each one, with links to the templates on GitHub:</span></span>

* [<span data-ttu-id="f5d06-113">Création d'un espace de noms Service Bus</span><span class="sxs-lookup"><span data-stu-id="f5d06-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
* [<span data-ttu-id="f5d06-114">Créer un espace de noms Service Bus avec file d’attente</span><span class="sxs-lookup"><span data-stu-id="f5d06-114">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
* [<span data-ttu-id="f5d06-115">Créer un espace de noms Service Bus par rubrique et abonnement</span><span class="sxs-lookup"><span data-stu-id="f5d06-115">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
* [<span data-ttu-id="f5d06-116">Créer un espace de noms Service Bus avec file d'attente et règle d’autorisation</span><span class="sxs-lookup"><span data-stu-id="f5d06-116">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
* [<span data-ttu-id="f5d06-117">Créer un modèle d’espace de noms Service Bus avec rubrique, abonnement et règle</span><span class="sxs-lookup"><span data-stu-id="f5d06-117">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a><span data-ttu-id="f5d06-118">Déployer avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5d06-118">Deploy with PowerShell</span></span>

<span data-ttu-id="f5d06-119">La procédure suivante décrit comment utiliser PowerShell pour déployer un modèle Azure Resource Manager qui crée un espace de noms Service Bus de niveau **Standard** et une file d’attente au sein de cet espace de noms.</span><span class="sxs-lookup"><span data-stu-id="f5d06-119">The following procedure describes how to use PowerShell to deploy an Azure Resource Manager template that creates a **Standard** tier Service Bus namespace, and a queue within that namespace.</span></span> <span data-ttu-id="f5d06-120">Cet exemple est basé sur le modèle [Créer un espace de noms Service Bus avec file d’attente](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue).</span><span class="sxs-lookup"><span data-stu-id="f5d06-120">This example is based on the [Create a Service Bus namespace with queue](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) template.</span></span> <span data-ttu-id="f5d06-121">Le flux de travail est approximativement le suivant :</span><span class="sxs-lookup"><span data-stu-id="f5d06-121">The approximate workflow is as follows:</span></span>

1. <span data-ttu-id="f5d06-122">Installez PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f5d06-122">Install PowerShell.</span></span>
2. <span data-ttu-id="f5d06-123">Créez le modèle et (éventuellement) un fichier de paramètres.</span><span class="sxs-lookup"><span data-stu-id="f5d06-123">Create the template and (optionally) a parameter file.</span></span>
3. <span data-ttu-id="f5d06-124">Dans PowerShell, connectez-vous à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="f5d06-124">In PowerShell, log in to your Azure account.</span></span>
4. <span data-ttu-id="f5d06-125">Créez un groupe de ressources s'il n'en existe pas.</span><span class="sxs-lookup"><span data-stu-id="f5d06-125">Create a new resource group if one does not exist.</span></span>
5. <span data-ttu-id="f5d06-126">Testez le déploiement.</span><span class="sxs-lookup"><span data-stu-id="f5d06-126">Test the deployment.</span></span>
6. <span data-ttu-id="f5d06-127">Si vous le souhaitez, définissez le mode de déploiement.</span><span class="sxs-lookup"><span data-stu-id="f5d06-127">If desired, set the deployment mode.</span></span>
7. <span data-ttu-id="f5d06-128">Déployez le modèle.</span><span class="sxs-lookup"><span data-stu-id="f5d06-128">Deploy the template.</span></span>

<span data-ttu-id="f5d06-129">Pour des informations complètes sur le déploiement de modèles Azure Resource Manager, consultez [Déployer des ressources à l’aide de modèles Azure Resource Manager][Deploy resources with Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="f5d06-129">For complete information about deploying Azure Resource Manager templates, see [Deploy resources with Azure Resource Manager templates][Deploy resources with Azure Resource Manager templates].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="f5d06-130">Installer PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5d06-130">Install PowerShell</span></span>

<span data-ttu-id="f5d06-131">Installez Azure PowerShell en suivant les instructions disponibles dans [Prise en main d’Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="f5d06-131">Install Azure PowerShell by following the instructions in [Getting started with Azure PowerShell](/powershell/azure/get-started-azureps).</span></span>

### <a name="create-a-template"></a><span data-ttu-id="f5d06-132">Créer un modèle</span><span class="sxs-lookup"><span data-stu-id="f5d06-132">Create a template</span></span>

<span data-ttu-id="f5d06-133">Clonez ou copiez le modèle [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) à partir de GitHub :</span><span class="sxs-lookup"><span data-stu-id="f5d06-133">Clone or copy the [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) template from GitHub:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of the Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of the Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by the template"
            }
        }
    },
    "variables": {
        "location": "[resourceGroup().location]",
        "sbVersion": "[parameters('serviceBusApiVersion')]",
        "defaultSASKeyName": "RootManageSharedAccessKey",
        "authRuleResourceId": "[resourceId('Microsoft.ServiceBus/namespaces/authorizationRules', parameters('serviceBusNamespaceName'), variables('defaultSASKeyName'))]"
    },
    "resources": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "resources": [{
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusQueueName')]",
            "type": "Queues",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusQueueName')]"
            }
        }]
    }],
    "outputs": {
        "NamespaceConnectionString": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryConnectionString]"
        },
        "SharedAccessPolicyPrimaryKey": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryKey]"
        }
    }
}
```

### <a name="create-a-parameters-file-optional"></a><span data-ttu-id="f5d06-134">Créer un fichier de paramètres (facultatif)</span><span class="sxs-lookup"><span data-stu-id="f5d06-134">Create a parameters file (optional)</span></span>

<span data-ttu-id="f5d06-135">Pour utiliser un fichier de paramètres facultatif, copiez le fichier [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json).</span><span class="sxs-lookup"><span data-stu-id="f5d06-135">To use an optional parameters file, copy the [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) file.</span></span> <span data-ttu-id="f5d06-136">Remplacez la valeur de `serviceBusNamespaceName` par le nom de l'espace de noms Service Bus que vous souhaitez créer dans ce déploiement, puis remplacez la valeur de `serviceBusQueueName` par le nom de la file d'attente que vous souhaitez créer.</span><span class="sxs-lookup"><span data-stu-id="f5d06-136">Replace the value of `serviceBusNamespaceName` with the name of the Service Bus namespace you want to create in this deployment, and replace the value of `serviceBusQueueName` with the name of the queue you want to create.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "value": "<myNamespaceName>"
        },
        "serviceBusQueueName": {
            "value": "<myQueueName>"
        },
        "serviceBusApiVersion": {
            "value": "2015-08-01"
        }
    }
}
```

<span data-ttu-id="f5d06-137">Pour plus d’informations, consultez la rubrique [aramètres](../azure-resource-manager/resource-group-template-deploy.md#parameter-files).</span><span class="sxs-lookup"><span data-stu-id="f5d06-137">For more information, see the [Parameters](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) topic.</span></span>

### <a name="log-in-to-azure-and-set-the-azure-subscription"></a><span data-ttu-id="f5d06-138">Se connecter à Azure et définir l’abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="f5d06-138">Log in to Azure and set the Azure subscription</span></span>

<span data-ttu-id="f5d06-139">À partir d’une invite de commandes PowerShell, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f5d06-139">From a PowerShell prompt, run the following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="f5d06-140">Vous êtes invité à ouvrir une session sur votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="f5d06-140">You are prompted to log on to your Azure account.</span></span> <span data-ttu-id="f5d06-141">Une fois connecté, exécutez la commande suivante pour afficher les abonnements disponibles.</span><span class="sxs-lookup"><span data-stu-id="f5d06-141">After logging on, run the following command to view your available subscriptions.</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="f5d06-142">Cette commande renvoie la liste des abonnements Azure disponibles.</span><span class="sxs-lookup"><span data-stu-id="f5d06-142">This command returns a list of available Azure subscriptions.</span></span> <span data-ttu-id="f5d06-143">Choisissez un abonnement pour la session en cours en exécutant la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="f5d06-143">Choose a subscription for the current session by running the following command.</span></span> <span data-ttu-id="f5d06-144">Remplacez `<YourSubscriptionId>` par le GUID de l’abonnement Azure que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="f5d06-144">Replace `<YourSubscriptionId>` with the GUID for the Azure subscription you want to use.</span></span>

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-the-resource-group"></a><span data-ttu-id="f5d06-145">Définir le groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="f5d06-145">Set the resource group</span></span>

<span data-ttu-id="f5d06-146">Si vous n’avez pas de groupe de ressources, créez-en un avec la commande **New-AzureRmResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="f5d06-146">If you do not have an existing resource group, create a new resource group with the **New-AzureRmResourceGroup ** command.</span></span> <span data-ttu-id="f5d06-147">Indiquez le nom du groupe de ressources et l'emplacement que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="f5d06-147">Provide the name of the resource group and location you want to use.</span></span> <span data-ttu-id="f5d06-148">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f5d06-148">For example:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

<span data-ttu-id="f5d06-149">En cas de réussite, un résumé du nouveau groupe de ressources s’affiche.</span><span class="sxs-lookup"><span data-stu-id="f5d06-149">If successful, a summary of the new resource group is displayed.</span></span>

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-the-deployment"></a><span data-ttu-id="f5d06-150">test du déploiement</span><span class="sxs-lookup"><span data-stu-id="f5d06-150">Test the deployment</span></span>

<span data-ttu-id="f5d06-151">Validez votre déploiement en exécutant l’applet de commande `Test-AzureRmResourceGroupDeployment`.</span><span class="sxs-lookup"><span data-stu-id="f5d06-151">Validate your deployment by running the `Test-AzureRmResourceGroupDeployment` cmdlet.</span></span> <span data-ttu-id="f5d06-152">Lorsque vous testez le déploiement, indiquez les paramètres exactement comme vous le feriez lors de l'exécution du déploiement.</span><span class="sxs-lookup"><span data-stu-id="f5d06-152">When testing the deployment, provide parameters exactly as you would when executing the deployment.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

### <a name="create-the-deployment"></a><span data-ttu-id="f5d06-153">Créer le déploiement</span><span class="sxs-lookup"><span data-stu-id="f5d06-153">Create the deployment</span></span>

<span data-ttu-id="f5d06-154">Pour créer le déploiement, exécutez l’applet de commande `New-AzureRmResourceGroupDeployment` et indiquez les paramètres nécessaires quand vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="f5d06-154">To create the new deployment, run the `New-AzureRmResourceGroupDeployment` cmdlet, and provide the necessary parameters when prompted.</span></span> <span data-ttu-id="f5d06-155">Les paramètres incluent un nom pour votre déploiement, le nom de votre groupe de ressources, le chemin d’accès ou l’URL du fichier de modèle.</span><span class="sxs-lookup"><span data-stu-id="f5d06-155">The parameters include a name for your deployment, the name of your resource group, and the path or URL to the template file.</span></span> <span data-ttu-id="f5d06-156">Si le paramètre **Mode** n’est pas spécifié, la valeur par défaut **Incremental** est utilisée.</span><span class="sxs-lookup"><span data-stu-id="f5d06-156">If the **Mode** parameter is not specified, the default value of **Incremental** is used.</span></span> <span data-ttu-id="f5d06-157">Pour plus d’informations, consultez [Déploiements incrémentiels et complets](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span><span class="sxs-lookup"><span data-stu-id="f5d06-157">For more information, see [Incremental and complete deployments](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span></span>

<span data-ttu-id="f5d06-158">La commande suivante vous invite à entrer les trois paramètres dans la fenêtre PowerShell :</span><span class="sxs-lookup"><span data-stu-id="f5d06-158">The following command prompts you for the three parameters in the PowerShell window:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

<span data-ttu-id="f5d06-159">Pour spécifier un fichier de paramètres à la place, utilisez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="f5d06-159">To specify a parameters file instead, use the following command.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json -TemplateParameterFile <path to parameters file>\azuredeploy.parameters.json
```

<span data-ttu-id="f5d06-160">Vous pouvez également utiliser des paramètres inclus lorsque vous exécutez l'applet de commande de déploiement.</span><span class="sxs-lookup"><span data-stu-id="f5d06-160">You can also use inline parameters when you run the deployment cmdlet.</span></span> <span data-ttu-id="f5d06-161">La commande est la suivante :</span><span class="sxs-lookup"><span data-stu-id="f5d06-161">The command is as follows:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json -parameterName "parameterValue"
```

<span data-ttu-id="f5d06-162">Pour exécuter un déploiement [complet](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments), affectez la valeur **Complet** au paramètre **Mode** :</span><span class="sxs-lookup"><span data-stu-id="f5d06-162">To run a [complete](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) deployment, set the **Mode** parameter to **Complete**:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

### <a name="verify-the-deployment"></a><span data-ttu-id="f5d06-163">Vérifier le déploiement</span><span class="sxs-lookup"><span data-stu-id="f5d06-163">Verify the deployment</span></span>
<span data-ttu-id="f5d06-164">Si les ressources sont déployées avec succès, un résumé du déploiement s’affiche dans la fenêtre PowerShell :</span><span class="sxs-lookup"><span data-stu-id="f5d06-164">If the resources are deployed successfully, a summary of the deployment is displayed in the PowerShell window:</span></span>

```powershell
DeploymentName    : MyDemoDeployment
ResourceGroupName : MyDemoRG
ProvisioningState : Succeeded
Timestamp         : 4/19/2016 10:38:30 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
                    Name             Type                       Value
                    ===============  =========================  ==========
                    serviceBusNamespaceName  String             <namespaceName>
                    serviceBusQueueName  String                 <queueName>
                    serviceBusApiVersion  String                2015-08-01

```

## <a name="next-steps"></a><span data-ttu-id="f5d06-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f5d06-165">Next steps</span></span>
<span data-ttu-id="f5d06-166">Vous avez maintenant vu le flux de travail et les commandes de base pour le déploiement d'un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f5d06-166">You've now seen the basic workflow and commands for deploying an Azure Resource Manager template.</span></span> <span data-ttu-id="f5d06-167">Pour plus d'informations, consultez les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="f5d06-167">For more detailed information, visit the following links:</span></span>

* <span data-ttu-id="f5d06-168">[Présentation d’Azure Resource Manager][Azure Resource Manager overview]</span><span class="sxs-lookup"><span data-stu-id="f5d06-168">[Azure Resource Manager overview][Azure Resource Manager overview]</span></span>
* <span data-ttu-id="f5d06-169">[Déployer des ressources à l’aide de modèles Resource Manager et d’Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span><span class="sxs-lookup"><span data-stu-id="f5d06-169">[Deploy resources with Resource Manager templates and Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span></span>
* [<span data-ttu-id="f5d06-170">Création de modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f5d06-170">Authoring Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
