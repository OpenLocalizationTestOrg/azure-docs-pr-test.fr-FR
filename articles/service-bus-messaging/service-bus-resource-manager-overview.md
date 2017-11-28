---
title: "ressources d’Azure Service Bus aaaCreate à l’aide de modèles Azure Resource Manager | Documents Microsoft"
description: "Utilisez Azure Resource Manager modèles tooautomate hello la création de ressources de Service Bus"
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
ms.openlocfilehash: e539902cae307b63ae7c332580e2064761331ec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a><span data-ttu-id="369bf-103">Création de ressources Service Bus à l’aide de modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="369bf-103">Create Service Bus resources using Azure Resource Manager templates</span></span>

<span data-ttu-id="369bf-104">Cet article décrit comment toocreate et déployer des ressources Service Bus à l’aide de modèles Azure Resource Manager, PowerShell et fournisseur de ressources de Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="369bf-104">This article describes how toocreate and deploy Service Bus resources using Azure Resource Manager templates, PowerShell, and hello Service Bus resource provider.</span></span>

<span data-ttu-id="369bf-105">Modèles de gestionnaire de ressources Azure vous permettent de définir toodeploy de ressources hello pour une solution et les paramètres toospecify et les variables qui vous permettent de valeurs tooinput pour différents environnements.</span><span class="sxs-lookup"><span data-stu-id="369bf-105">Azure Resource Manager templates help you define hello resources toodeploy for a solution, and toospecify parameters and variables that enable you tooinput values for different environments.</span></span> <span data-ttu-id="369bf-106">modèle de Hello se compose de JSON et les expressions que vous pouvez utiliser les valeurs tooconstruct pour votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="369bf-106">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="369bf-107">Pour plus d’informations sur l’écriture de modèles Azure Resource Manager et une description de format de modèle hello, consultez [structure et la syntaxe des modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="369bf-107">For detailed information about writing Azure Resource Manager templates, and a discussion of hello template format, see [structure and syntax of Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

> [!NOTE]
> <span data-ttu-id="369bf-108">Hello les exemples de cette montrent l’article comment toouse Azure Resource Manager toocreate un espace de noms Service Bus et la messagerie de l’entité (file d’attente).</span><span class="sxs-lookup"><span data-stu-id="369bf-108">hello examples in this article show how toouse Azure Resource Manager toocreate a Service Bus namespace and messaging entity (queue).</span></span> <span data-ttu-id="369bf-109">Pour obtenir des exemples de modèle, visitez hello [la galerie de modèles de démarrage rapide Azure] [ Azure Quickstart Templates gallery] et recherchez « Service Bus ».</span><span class="sxs-lookup"><span data-stu-id="369bf-109">For other template examples, visit hello [Azure Quickstart Templates gallery][Azure Quickstart Templates gallery] and search for "Service Bus."</span></span>
>
>

## <a name="service-bus-resource-manager-templates"></a><span data-ttu-id="369bf-110">Modèles Resource Manager Service Bus</span><span class="sxs-lookup"><span data-stu-id="369bf-110">Service Bus Resource Manager templates</span></span>

<span data-ttu-id="369bf-111">Ces modèles Azure Resource Manager Service Bus sont disponibles au téléchargement et au déploiement.</span><span class="sxs-lookup"><span data-stu-id="369bf-111">These Service Bus Azure Resource Manager templates are available for download and deployment.</span></span> <span data-ttu-id="369bf-112">Cliquez sur hello suivant les liens pour plus d’informations sur chacune d’elles, avec des modèles de toohello de liens sur GitHub :</span><span class="sxs-lookup"><span data-stu-id="369bf-112">Click hello following links for details about each one, with links toohello templates on GitHub:</span></span>

* [<span data-ttu-id="369bf-113">Création d'un espace de noms Service Bus</span><span class="sxs-lookup"><span data-stu-id="369bf-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
* [<span data-ttu-id="369bf-114">Créer un espace de noms Service Bus avec file d’attente</span><span class="sxs-lookup"><span data-stu-id="369bf-114">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
* [<span data-ttu-id="369bf-115">Créer un espace de noms Service Bus par rubrique et abonnement</span><span class="sxs-lookup"><span data-stu-id="369bf-115">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
* [<span data-ttu-id="369bf-116">Créer un espace de noms Service Bus avec file d'attente et règle d’autorisation</span><span class="sxs-lookup"><span data-stu-id="369bf-116">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
* [<span data-ttu-id="369bf-117">Créer un modèle d’espace de noms Service Bus avec rubrique, abonnement et règle</span><span class="sxs-lookup"><span data-stu-id="369bf-117">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a><span data-ttu-id="369bf-118">Déployer avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="369bf-118">Deploy with PowerShell</span></span>

<span data-ttu-id="369bf-119">Hello procédure suivante décrit comment toouse PowerShell toodeploy un modèle Azure Resource Manager qui crée un **Standard** de niveau espace de noms Service Bus et une file d’attente au sein de cet espace de noms.</span><span class="sxs-lookup"><span data-stu-id="369bf-119">hello following procedure describes how toouse PowerShell toodeploy an Azure Resource Manager template that creates a **Standard** tier Service Bus namespace, and a queue within that namespace.</span></span> <span data-ttu-id="369bf-120">Cet exemple est basé sur hello [créer un espace de noms Service Bus avec la file d’attente](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) modèle.</span><span class="sxs-lookup"><span data-stu-id="369bf-120">This example is based on hello [Create a Service Bus namespace with queue](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) template.</span></span> <span data-ttu-id="369bf-121">flux de travail approximatif Hello est comme suit :</span><span class="sxs-lookup"><span data-stu-id="369bf-121">hello approximate workflow is as follows:</span></span>

1. <span data-ttu-id="369bf-122">Installez PowerShell.</span><span class="sxs-lookup"><span data-stu-id="369bf-122">Install PowerShell.</span></span>
2. <span data-ttu-id="369bf-123">Créer le modèle de hello et (facultativement) d’un fichier de paramètres.</span><span class="sxs-lookup"><span data-stu-id="369bf-123">Create hello template and (optionally) a parameter file.</span></span>
3. <span data-ttu-id="369bf-124">Dans PowerShell, connectez-vous tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="369bf-124">In PowerShell, log in tooyour Azure account.</span></span>
4. <span data-ttu-id="369bf-125">Créez un groupe de ressources s'il n'en existe pas.</span><span class="sxs-lookup"><span data-stu-id="369bf-125">Create a new resource group if one does not exist.</span></span>
5. <span data-ttu-id="369bf-126">Tester le déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="369bf-126">Test hello deployment.</span></span>
6. <span data-ttu-id="369bf-127">Si vous le souhaitez, définissez le mode de déploiement hello.</span><span class="sxs-lookup"><span data-stu-id="369bf-127">If desired, set hello deployment mode.</span></span>
7. <span data-ttu-id="369bf-128">Déployer le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="369bf-128">Deploy hello template.</span></span>

<span data-ttu-id="369bf-129">Pour des informations complètes sur le déploiement de modèles Azure Resource Manager, consultez [Déployer des ressources à l’aide de modèles Azure Resource Manager][Deploy resources with Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="369bf-129">For complete information about deploying Azure Resource Manager templates, see [Deploy resources with Azure Resource Manager templates][Deploy resources with Azure Resource Manager templates].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="369bf-130">Installer PowerShell</span><span class="sxs-lookup"><span data-stu-id="369bf-130">Install PowerShell</span></span>

<span data-ttu-id="369bf-131">Installez Azure PowerShell en suivant les instructions de hello dans [prise en main d’Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="369bf-131">Install Azure PowerShell by following hello instructions in [Getting started with Azure PowerShell](/powershell/azure/get-started-azureps).</span></span>

### <a name="create-a-template"></a><span data-ttu-id="369bf-132">Créer un modèle</span><span class="sxs-lookup"><span data-stu-id="369bf-132">Create a template</span></span>

<span data-ttu-id="369bf-133">Clone ou copie hello [201-servicebus-créer-file d’attente](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) modèle à partir de GitHub :</span><span class="sxs-lookup"><span data-stu-id="369bf-133">Clone or copy hello [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) template from GitHub:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by hello template"
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

### <a name="create-a-parameters-file-optional"></a><span data-ttu-id="369bf-134">Créer un fichier de paramètres (facultatif)</span><span class="sxs-lookup"><span data-stu-id="369bf-134">Create a parameters file (optional)</span></span>

<span data-ttu-id="369bf-135">toouse un fichier de paramètres facultatifs, hello de copie [201-servicebus-créer-file d’attente](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) fichier.</span><span class="sxs-lookup"><span data-stu-id="369bf-135">toouse an optional parameters file, copy hello [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) file.</span></span> <span data-ttu-id="369bf-136">Remplacez la valeur hello `serviceBusNamespaceName` avec nom hello d’espace de noms Service Bus hello votre choix toocreate dans ce déploiement, remplacez la valeur hello `serviceBusQueueName` avec nom hello de file d’attente hello souhaité toocreate.</span><span class="sxs-lookup"><span data-stu-id="369bf-136">Replace hello value of `serviceBusNamespaceName` with hello name of hello Service Bus namespace you want toocreate in this deployment, and replace hello value of `serviceBusQueueName` with hello name of hello queue you want toocreate.</span></span>

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

<span data-ttu-id="369bf-137">Pour plus d’informations, consultez hello [paramètres](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) rubrique.</span><span class="sxs-lookup"><span data-stu-id="369bf-137">For more information, see hello [Parameters](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) topic.</span></span>

### <a name="log-in-tooazure-and-set-hello-azure-subscription"></a><span data-ttu-id="369bf-138">Connectez-vous à tooAzure et définir hello abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="369bf-138">Log in tooAzure and set hello Azure subscription</span></span>

<span data-ttu-id="369bf-139">À partir d’une invite de PowerShell, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="369bf-139">From a PowerShell prompt, run hello following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="369bf-140">Vous êtes invité à toolog sur tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="369bf-140">You are prompted toolog on tooyour Azure account.</span></span> <span data-ttu-id="369bf-141">Après l’ouverture de session, exécutez hello suivant commande tooview vos abonnements disponibles.</span><span class="sxs-lookup"><span data-stu-id="369bf-141">After logging on, run hello following command tooview your available subscriptions.</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="369bf-142">Cette commande renvoie la liste des abonnements Azure disponibles.</span><span class="sxs-lookup"><span data-stu-id="369bf-142">This command returns a list of available Azure subscriptions.</span></span> <span data-ttu-id="369bf-143">Choisissez un abonnement pour hello session en cours en exécutant hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="369bf-143">Choose a subscription for hello current session by running hello following command.</span></span> <span data-ttu-id="369bf-144">Remplacez `<YourSubscriptionId>` par hello GUID pour hello abonnement Azure, vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="369bf-144">Replace `<YourSubscriptionId>` with hello GUID for hello Azure subscription you want toouse.</span></span>

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-hello-resource-group"></a><span data-ttu-id="369bf-145">Définir le groupe de ressources hello</span><span class="sxs-lookup"><span data-stu-id="369bf-145">Set hello resource group</span></span>

<span data-ttu-id="369bf-146">Si vous n’avez pas une ressource existante, créer un groupe de ressources avec hello ** New-AzureRmResourceGroup ** commande.</span><span class="sxs-lookup"><span data-stu-id="369bf-146">If you do not have an existing resource group, create a new resource group with hello **New-AzureRmResourceGroup ** command.</span></span> <span data-ttu-id="369bf-147">Fournir le nom hello du groupe de ressources hello et un emplacement toouse.</span><span class="sxs-lookup"><span data-stu-id="369bf-147">Provide hello name of hello resource group and location you want toouse.</span></span> <span data-ttu-id="369bf-148">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="369bf-148">For example:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

<span data-ttu-id="369bf-149">En cas de réussite, un résumé du nouveau groupe de ressources hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="369bf-149">If successful, a summary of hello new resource group is displayed.</span></span>

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-hello-deployment"></a><span data-ttu-id="369bf-150">Déploiement de test hello</span><span class="sxs-lookup"><span data-stu-id="369bf-150">Test hello deployment</span></span>

<span data-ttu-id="369bf-151">Valider votre déploiement en exécutant hello `Test-AzureRmResourceGroupDeployment` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="369bf-151">Validate your deployment by running hello `Test-AzureRmResourceGroupDeployment` cmdlet.</span></span> <span data-ttu-id="369bf-152">Lorsque vous testez le déploiement de hello, spécifiez les paramètres exactement comme vous le feriez lors de l’exécution du déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="369bf-152">When testing hello deployment, provide parameters exactly as you would when executing hello deployment.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="create-hello-deployment"></a><span data-ttu-id="369bf-153">Créer le déploiement de hello</span><span class="sxs-lookup"><span data-stu-id="369bf-153">Create hello deployment</span></span>

<span data-ttu-id="369bf-154">toocreate hello nouveau déploiement, exécutez hello `New-AzureRmResourceGroupDeployment` applet de commande et fournir les paramètres nécessaires hello lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="369bf-154">toocreate hello new deployment, run hello `New-AzureRmResourceGroupDeployment` cmdlet, and provide hello necessary parameters when prompted.</span></span> <span data-ttu-id="369bf-155">les paramètres de Hello incluent un nom pour votre déploiement, le nom de votre groupe de ressources et le chemin d’accès hello ou le fichier de modèle d’URL toohello de hello.</span><span class="sxs-lookup"><span data-stu-id="369bf-155">hello parameters include a name for your deployment, hello name of your resource group, and hello path or URL toohello template file.</span></span> <span data-ttu-id="369bf-156">Si hello **Mode** paramètre n’est pas spécifié, hello la valeur par défaut de **incrémentiel** est utilisé.</span><span class="sxs-lookup"><span data-stu-id="369bf-156">If hello **Mode** parameter is not specified, hello default value of **Incremental** is used.</span></span> <span data-ttu-id="369bf-157">Pour plus d’informations, consultez [Déploiements incrémentiels et complets](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span><span class="sxs-lookup"><span data-stu-id="369bf-157">For more information, see [Incremental and complete deployments](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span></span>

<span data-ttu-id="369bf-158">Hello après les invites de commandes vous pour les paramètres dans la fenêtre de PowerShell hello hello trois :</span><span class="sxs-lookup"><span data-stu-id="369bf-158">hello following command prompts you for hello three parameters in hello PowerShell window:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

<span data-ttu-id="369bf-159">toospecify un fichier de paramètres, utilisez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="369bf-159">toospecify a parameters file instead, use hello following command.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -TemplateParameterFile <path tooparameters file>\azuredeploy.parameters.json
```

<span data-ttu-id="369bf-160">Vous pouvez également utiliser des paramètres inclus lorsque vous exécutez l’applet de commande de déploiement hello.</span><span class="sxs-lookup"><span data-stu-id="369bf-160">You can also use inline parameters when you run hello deployment cmdlet.</span></span> <span data-ttu-id="369bf-161">commande Hello est comme suit :</span><span class="sxs-lookup"><span data-stu-id="369bf-161">hello command is as follows:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -parameterName "parameterValue"
```

<span data-ttu-id="369bf-162">toorun un [complète](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) hello d’ensemble du déploiement, **Mode** paramètre trop**Complete**:</span><span class="sxs-lookup"><span data-stu-id="369bf-162">toorun a [complete](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) deployment, set hello **Mode** parameter too**Complete**:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="verify-hello-deployment"></a><span data-ttu-id="369bf-163">Vérifier le déploiement de hello</span><span class="sxs-lookup"><span data-stu-id="369bf-163">Verify hello deployment</span></span>
<span data-ttu-id="369bf-164">Si les ressources hello sont déployées avec succès, un résumé du déploiement de hello s’affiche dans la fenêtre de PowerShell hello :</span><span class="sxs-lookup"><span data-stu-id="369bf-164">If hello resources are deployed successfully, a summary of hello deployment is displayed in hello PowerShell window:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="369bf-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="369bf-165">Next steps</span></span>
<span data-ttu-id="369bf-166">Vous avez maintenant vu des flux de travail hello et les commandes pour le déploiement d’un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="369bf-166">You've now seen hello basic workflow and commands for deploying an Azure Resource Manager template.</span></span> <span data-ttu-id="369bf-167">Pour plus d’informations, visitez hello suivant liens :</span><span class="sxs-lookup"><span data-stu-id="369bf-167">For more detailed information, visit hello following links:</span></span>

* <span data-ttu-id="369bf-168">[Présentation d’Azure Resource Manager][Azure Resource Manager overview]</span><span class="sxs-lookup"><span data-stu-id="369bf-168">[Azure Resource Manager overview][Azure Resource Manager overview]</span></span>
* <span data-ttu-id="369bf-169">[Déployer des ressources à l’aide de modèles Resource Manager et d’Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span><span class="sxs-lookup"><span data-stu-id="369bf-169">[Deploy resources with Resource Manager templates and Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span></span>
* [<span data-ttu-id="369bf-170">Création de modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="369bf-170">Authoring Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
