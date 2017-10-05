---
title: "Créer un espace de noms Azure Service Bus ainsi qu’une rubrique et un abonnement à l’aide d’un modèle Azure Resource Manager | Microsoft Docs"
description: "Créer un espace de noms Service Bus par rubrique et abonnement à l’aide d’un modèle Azure Resource Manager"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d3d55200-5c60-4b5f-822d-59974cafff0e
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 8dd48787e7b788d249085b3110484de1a2c1d265
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-bus-namespace-with-topic-and-subscription-using-an-azure-resource-manager-template"></a><span data-ttu-id="3b3c1-103">Créer un espace de noms Service Bus par rubrique et abonnement à l’aide d’un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3b3c1-103">Create a Service Bus namespace with topic and subscription using an Azure Resource Manager template</span></span>

<span data-ttu-id="3b3c1-104">Cet article montre comment utiliser un modèle Azure Resource Manager qui crée un espace de noms Service Bus ainsi qu’une rubrique et un abonnement au sein de cet espace de noms.</span><span class="sxs-lookup"><span data-stu-id="3b3c1-104">This article shows how to use an Azure Resource Manager template that creates a Service Bus namespace and a topic and subscription within that namespace.</span></span> <span data-ttu-id="3b3c1-105">Vous allez apprendre comment définir les ressources à déployer et configurer les paramètres qui sont spécifiés lors de l’exécution du déploiement.</span><span class="sxs-lookup"><span data-stu-id="3b3c1-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="3b3c1-106">Vous pouvez utiliser ce modèle pour vos propres déploiements, ou le personnaliser afin qu’il réponde à vos besoins</span><span class="sxs-lookup"><span data-stu-id="3b3c1-106">You can use this template for your own deployments, or customize it to meet your requirements</span></span>

<span data-ttu-id="3b3c1-107">Pour en savoir plus sur la création de modèles, consultez [Création de modèles Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="3b3c1-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="3b3c1-108">Pour le modèle complet, consultez le modèle [Espace de noms Service Bus avec rubrique et abonnement][Service Bus namespace with topic and subscription].</span><span class="sxs-lookup"><span data-stu-id="3b3c1-108">For the complete template, see the [Service Bus namespace with topic and subscription][Service Bus namespace with topic and subscription] template.</span></span>

> [!NOTE]
> <span data-ttu-id="3b3c1-109">Les modèles Azure Resource Manager suivants sont disponibles au téléchargement et au déploiement.</span><span class="sxs-lookup"><span data-stu-id="3b3c1-109">The following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="3b3c1-110">Création d'un espace de noms Service Bus</span><span class="sxs-lookup"><span data-stu-id="3b3c1-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="3b3c1-111">Créer un espace de noms Service Bus avec file d’attente</span><span class="sxs-lookup"><span data-stu-id="3b3c1-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="3b3c1-112">Créer un espace de noms Service Bus avec file d'attente et règle d’autorisation</span><span class="sxs-lookup"><span data-stu-id="3b3c1-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="3b3c1-113">Créer un modèle d’espace de noms Service Bus avec rubrique, abonnement et règle</span><span class="sxs-lookup"><span data-stu-id="3b3c1-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="3b3c1-114">Pour rechercher les derniers modèles, recherchez « Service Bus » dans la galerie [Modèles de démarrage rapide Azure][Azure Quickstart Templates].</span><span class="sxs-lookup"><span data-stu-id="3b3c1-114">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="3b3c1-115">Qu'allez-vous déployer ?</span><span class="sxs-lookup"><span data-stu-id="3b3c1-115">What will you deploy?</span></span>

<span data-ttu-id="3b3c1-116">Avec ce modèle, vous allez déployer un espace de noms Service Bus par rubrique et abonnement.</span><span class="sxs-lookup"><span data-stu-id="3b3c1-116">With this template, you will deploy a Service Bus namespace with topic and subscription.</span></span>

<span data-ttu-id="3b3c1-117">Les [rubriques et les abonnements Service Bus](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) fournissent une forme de communication de type un-à-plusieurs dans un modèle de *publication/abonnement*.</span><span class="sxs-lookup"><span data-stu-id="3b3c1-117">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span>

<span data-ttu-id="3b3c1-118">Pour exécuter automatiquement le déploiement, cliquez sur le bouton ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="3b3c1-118">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="3b3c1-119">[![Déploiement sur Azure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="3b3c1-119">[![Deploy to Azure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="3b3c1-120">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3b3c1-120">Parameters</span></span>

<span data-ttu-id="3b3c1-121">Azure Resource Manager vous permet de définir des paramètres pour les valeurs que vous voulez spécifier lorsque le modèle est déployé.</span><span class="sxs-lookup"><span data-stu-id="3b3c1-121">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="3b3c1-122">Ce modèle inclut une section appelée `Parameters` , qui contient toutes les valeurs de paramètres.</span><span class="sxs-lookup"><span data-stu-id="3b3c1-122">The template includes a section called `Parameters` that contains all of the parameter values.</span></span> <span data-ttu-id="3b3c1-123">Vous devez définir un paramètre pour les valeurs qui varient selon le projet que vous déployez, ou de l’environnement dans lequel vous effectuez le déploiement.</span><span class="sxs-lookup"><span data-stu-id="3b3c1-123">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="3b3c1-124">Ne définissez pas de paramètres pour les valeurs qui restent identiques.</span><span class="sxs-lookup"><span data-stu-id="3b3c1-124">Do not define parameters for values that will always stay the same.</span></span> <span data-ttu-id="3b3c1-125">Chaque valeur de paramètre est utilisée dans le modèle pour définir les ressources déployées.</span><span class="sxs-lookup"><span data-stu-id="3b3c1-125">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="3b3c1-126">Le modèle définit les paramètres suivants.</span><span class="sxs-lookup"><span data-stu-id="3b3c1-126">The template defines the following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="3b3c1-127">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="3b3c1-127">serviceBusNamespaceName</span></span>
<span data-ttu-id="3b3c1-128">Nom de l’espace de noms Service Bus à créer.</span><span class="sxs-lookup"><span data-stu-id="3b3c1-128">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="3b3c1-129">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="3b3c1-129">serviceBusTopicName</span></span>
<span data-ttu-id="3b3c1-130">Nom de la rubrique créée dans l’espace de noms Service Bus.</span><span class="sxs-lookup"><span data-stu-id="3b3c1-130">The name of the topic created in the Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="3b3c1-131">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="3b3c1-131">serviceBusSubscriptionName</span></span>
<span data-ttu-id="3b3c1-132">Nom de l'abonnement créé dans l'espace de noms Service Bus.</span><span class="sxs-lookup"><span data-stu-id="3b3c1-132">The name of the subscription created in the Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="3b3c1-133">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="3b3c1-133">serviceBusApiVersion</span></span>
<span data-ttu-id="3b3c1-134">La version de l’API Service Bus du modèle.</span><span class="sxs-lookup"><span data-stu-id="3b3c1-134">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-to-deploy"></a><span data-ttu-id="3b3c1-135">Ressources à déployer</span><span class="sxs-lookup"><span data-stu-id="3b3c1-135">Resources to deploy</span></span>
<span data-ttu-id="3b3c1-136">Crée un espace de noms Service Bus standard de type **Messagerie**, par rubrique et abonnement.</span><span class="sxs-lookup"><span data-stu-id="3b3c1-136">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription.</span></span>

```json
"resources ": [{
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
            "name": "[parameters('serviceBusTopicName')]",
            "type": "Topics",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusTopicName')]",
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {}
            }]
        }]
    }]
```

## <a name="commands-to-run-deployment"></a><span data-ttu-id="3b3c1-137">Commandes pour exécuter le déploiement</span><span class="sxs-lookup"><span data-stu-id="3b3c1-137">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="3b3c1-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b3c1-138">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="3b3c1-139">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="3b3c1-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="3b3c1-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3b3c1-140">Next steps</span></span>
<span data-ttu-id="3b3c1-141">Maintenant que vous avez créé et déployé des ressources à l’aide d’Azure Resource Manager, découvrez comment gérer ces ressources en consultant les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="3b3c1-141">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="3b3c1-142">Gestion de Service Bus avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b3c1-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="3b3c1-143">Gérer les ressources Service Bus avec l'explorateur Service Bus</span><span class="sxs-lookup"><span data-stu-id="3b3c1-143">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus namespace with topic and subscription]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-and-subscription/
