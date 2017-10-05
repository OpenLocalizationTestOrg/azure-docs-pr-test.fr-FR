---
title: "Créer un abonnement Azure Service Bus ainsi qu’une règle à l’aide d’un modèle Azure Resource Manager | Microsoft Docs"
description: "Créer un espace de noms Service Bus avec rubrique, abonnement et règle à l’aide d’un modèle Azure Resource Manager"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9e0aaf58-0214-4bca-bd00-d29c08f9b1bc
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 35e67d86b42358c4ce28b41beae1ee8e1896e939
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-bus-namespace-with-topic-subscription-and-rule-using-an-azure-resource-manager-template"></a><span data-ttu-id="14762-103">Créer un espace de noms Service Bus avec rubrique, abonnement et règle à l’aide d’un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="14762-103">Create a Service Bus namespace with topic, subscription, and rule using an Azure Resource Manager template</span></span>

<span data-ttu-id="14762-104">Cet article montre comment utiliser un modèle Azure Resource Manager qui crée un espace de noms Service Bus avec une rubrique, un abonnement et une règle (filtre).</span><span class="sxs-lookup"><span data-stu-id="14762-104">This article shows how to use an Azure Resource Manager template that creates a Service Bus namespace with a topic, subscription, and rule (filter).</span></span> <span data-ttu-id="14762-105">Vous apprenez à définir les ressources à déployer et à configurer les paramètres qui sont spécifiés lors de l’exécution du déploiement.</span><span class="sxs-lookup"><span data-stu-id="14762-105">You learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="14762-106">Vous pouvez utiliser ce modèle pour vos propres déploiements, ou le personnaliser afin qu’il réponde à vos besoins</span><span class="sxs-lookup"><span data-stu-id="14762-106">You can use this template for your own deployments, or customize it to meet your requirements</span></span>

<span data-ttu-id="14762-107">Pour plus d’informations sur la création de modèles, consultez [Création de modèles Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="14762-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="14762-108">Pour plus d’informations sur les pratiques et les modèles des conventions d’affectation de noms des ressources Azure, consultez [Conventions d’affectation de noms recommandées pour les ressources Azure][Recommended naming conventions for Azure resources].</span><span class="sxs-lookup"><span data-stu-id="14762-108">For more information about practice and patterns on Azure resources naming conventions, see [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources].</span></span>

<span data-ttu-id="14762-109">Pour obtenir le modèle complet, consultez le [modèle d’espace de noms Service Bus avec rubrique, abonnement et règle][Service Bus namespace with topic, subscription, and rule].</span><span class="sxs-lookup"><span data-stu-id="14762-109">For the complete template, see the [Service Bus namespace with topic, subscription, and rule][Service Bus namespace with topic, subscription, and rule] template.</span></span>

> [!NOTE]
> <span data-ttu-id="14762-110">Les modèles Azure Resource Manager suivants sont disponibles au téléchargement et au déploiement.</span><span class="sxs-lookup"><span data-stu-id="14762-110">The following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="14762-111">Créer un espace de noms Service Bus avec file d'attente et règle d’autorisation</span><span class="sxs-lookup"><span data-stu-id="14762-111">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="14762-112">Créer un espace de noms Service Bus avec file d’attente</span><span class="sxs-lookup"><span data-stu-id="14762-112">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="14762-113">Création d'un espace de noms Service Bus</span><span class="sxs-lookup"><span data-stu-id="14762-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="14762-114">Créer un espace de noms Service Bus par rubrique et abonnement</span><span class="sxs-lookup"><span data-stu-id="14762-114">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> 
> <span data-ttu-id="14762-115">Pour rechercher les derniers modèles, recherchez « Service Bus » dans la galerie [Modèles de démarrage rapide Azure][Azure Quickstart Templates].</span><span class="sxs-lookup"><span data-stu-id="14762-115">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="14762-116">Qu'allez-vous déployer ?</span><span class="sxs-lookup"><span data-stu-id="14762-116">What will you deploy?</span></span>

<span data-ttu-id="14762-117">Avec ce modèle, vous déployez un espace de noms Service Bus avec rubrique, abonnement et règle (filtre).</span><span class="sxs-lookup"><span data-stu-id="14762-117">With this template, you deploy a Service Bus namespace with topic, subscription, and rule (filter).</span></span>

<span data-ttu-id="14762-118">Les [rubriques et les abonnements Service Bus](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) fournissent une forme de communication de type un-à-plusieurs dans un modèle de *publication/abonnement*.</span><span class="sxs-lookup"><span data-stu-id="14762-118">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span> <span data-ttu-id="14762-119">Lorsque vous utilisez des rubriques et des abonnements, les composants d’une application distribuée ne communiquent pas directement les uns avec les autres : ils échangent des messages par le biais d’une rubrique qui fait office d’intermédiaire. Un abonnement à une rubrique ressemble à une file d’attente virtuelle qui reçoit des copies des messages envoyés à la rubrique. Un abonnement à une rubrique ressemble à une file d’attente virtuelle qui reçoit des copies des messages envoyés à la rubrique.</span><span class="sxs-lookup"><span data-stu-id="14762-119">When using topics and subscriptions, components of a distributed application do not communicate directly with each other, instead they exchange messages via topic that acts as an intermediary.A subscription to a topic resembles a virtual queue that receives copies of messages that were sent to the topic.</span></span> <span data-ttu-id="14762-120">Une filtre sur un abonnement vous permet de spécifier quels sont les messages, parmi ceux envoyés à une rubrique, qui doivent apparaître dans un abonnement de rubrique spécifique.</span><span class="sxs-lookup"><span data-stu-id="14762-120">A filter on subscription enables you to specify which messages sent to a topic should appear within a specific topic subscription.</span></span>

## <a name="what-are-rules-filters"></a><span data-ttu-id="14762-121">Qu’est-ce qu’une règle (filtre) ?</span><span class="sxs-lookup"><span data-stu-id="14762-121">What are rules (filters)?</span></span>

<span data-ttu-id="14762-122">Dans de nombreux scénarios, les messages ayant des caractéristiques spécifiques doivent être traités différemment.</span><span class="sxs-lookup"><span data-stu-id="14762-122">In many scenarios, messages that have specific characteristics must be processed in different ways.</span></span> <span data-ttu-id="14762-123">Pour ce faire, vous pouvez configurer des abonnements pour rechercher les messages présentant les propriétés spécifiques, puis apporter des modifications à ces propriétés.</span><span class="sxs-lookup"><span data-stu-id="14762-123">To enable this, you can configure subscriptions to find messages that have specific properties and then perform modifications to those properties.</span></span> <span data-ttu-id="14762-124">Bien que les abonnements Service Bus voient tous les messages envoyés à la rubrique, vous pouvez uniquement copier un sous-ensemble de ces messages dans la file d’attente d’abonnement virtuelle.</span><span class="sxs-lookup"><span data-stu-id="14762-124">Although Service Bus subscriptions see all messages sent to the topic, you can only copy a subset of those messages to the virtual subscription queue.</span></span> <span data-ttu-id="14762-125">Pour ce faire, il faut utiliser des filtres d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="14762-125">This is accomplished using subscription filters.</span></span> <span data-ttu-id="14762-126">Pour en savoir plus sur les règles (filtres), consultez [Règles et actions](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span><span class="sxs-lookup"><span data-stu-id="14762-126">To learn more about rules (filters), see [Rules and actions](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span></span>

<span data-ttu-id="14762-127">Pour exécuter automatiquement le déploiement, cliquez sur le bouton ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="14762-127">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="14762-128">[![Déploiement sur Azure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="14762-128">[![Deploy to Azure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="14762-129">Paramètres</span><span class="sxs-lookup"><span data-stu-id="14762-129">Parameters</span></span>

<span data-ttu-id="14762-130">Avec Azure Resource Manager, vous devez définir des paramètres pour les valeurs que vous voulez spécifier lorsque le modèle est déployé.</span><span class="sxs-lookup"><span data-stu-id="14762-130">With Azure Resource Manager, you should define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="14762-131">Ce modèle inclut une section appelée `Parameters` , qui contient toutes les valeurs des paramètres.</span><span class="sxs-lookup"><span data-stu-id="14762-131">The template includes a section called `Parameters` that contains all the parameter values.</span></span> <span data-ttu-id="14762-132">Vous devez définir un paramètre pour les valeurs qui varient en fonction du projet que vous déployez ou de l’environnement dans lequel vous effectuez le déploiement.</span><span class="sxs-lookup"><span data-stu-id="14762-132">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="14762-133">Ne définissez pas de paramètres pour les valeurs qui restent inchangées.</span><span class="sxs-lookup"><span data-stu-id="14762-133">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="14762-134">Chaque valeur de paramètre est utilisée dans le modèle pour définir les ressources déployées.</span><span class="sxs-lookup"><span data-stu-id="14762-134">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="14762-135">Le modèle définit les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="14762-135">The template defines the following parameters:</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="14762-136">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="14762-136">serviceBusNamespaceName</span></span>
<span data-ttu-id="14762-137">Nom de l’espace de noms Service Bus à créer.</span><span class="sxs-lookup"><span data-stu-id="14762-137">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="14762-138">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="14762-138">serviceBusTopicName</span></span>
<span data-ttu-id="14762-139">Nom de la rubrique créée dans l’espace de noms Service Bus.</span><span class="sxs-lookup"><span data-stu-id="14762-139">The name of the topic created in the Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="14762-140">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="14762-140">serviceBusSubscriptionName</span></span>
<span data-ttu-id="14762-141">Nom de l'abonnement créé dans l'espace de noms Service Bus.</span><span class="sxs-lookup"><span data-stu-id="14762-141">The name of the subscription created in the Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```
### <a name="servicebusrulename"></a><span data-ttu-id="14762-142">serviceBusRuleName</span><span class="sxs-lookup"><span data-stu-id="14762-142">serviceBusRuleName</span></span>
<span data-ttu-id="14762-143">Nom de la règle (filtre) créée dans l’espace de noms Service Bus.</span><span class="sxs-lookup"><span data-stu-id="14762-143">The name of the rule(filter) created in the Service Bus namespace.</span></span>

```json
   "serviceBusRuleName": {
   "type": "string",
  }
```
### <a name="servicebusapiversion"></a><span data-ttu-id="14762-144">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="14762-144">serviceBusApiVersion</span></span>
<span data-ttu-id="14762-145">La version de l’API Service Bus du modèle.</span><span class="sxs-lookup"><span data-stu-id="14762-145">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-to-deploy"></a><span data-ttu-id="14762-146">Ressources à déployer</span><span class="sxs-lookup"><span data-stu-id="14762-146">Resources to deploy</span></span>
<span data-ttu-id="14762-147">Crée un espace de noms Service Bus standard de type **Messagerie**, avec rubrique, abonnement et règles.</span><span class="sxs-lookup"><span data-stu-id="14762-147">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription and rules.</span></span>

```json
 "resources": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "sku": {
            "name": "Standard",
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
                "path": "[parameters('serviceBusTopicName')]"
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {},
                "resources": [{
                    "apiVersion": "[variables('sbVersion')]",
                    "name": "[parameters('serviceBusRuleName')]",
                    "type": "Rules",
                    "dependsOn": [
                        "[parameters('serviceBusSubscriptionName')]"
                    ],
                    "properties": {
                        "filter": {
                            "sqlExpression": "StoreName = 'Store1'"
                        },
                        "action": {
                            "sqlExpression": "set FilterTag = 'true'"
                        }
                    }
                }]
            }]
        }]
    }]
```

## <a name="commands-to-run-deployment"></a><span data-ttu-id="14762-148">Commandes pour exécuter le déploiement</span><span class="sxs-lookup"><span data-stu-id="14762-148">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="14762-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="14762-149">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="14762-150">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="14762-150">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="14762-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="14762-151">Next steps</span></span>
<span data-ttu-id="14762-152">Maintenant que vous avez créé et déployé des ressources à l’aide d’Azure Resource Manager, découvrez comment gérer ces ressources en consultant les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="14762-152">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="14762-153">Gérer Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="14762-153">Manage Azure Service Bus</span></span>](service-bus-management-libraries.md)
* [<span data-ttu-id="14762-154">Gestion de Service Bus avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="14762-154">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="14762-155">Gérer les ressources Service Bus avec l'explorateur Service Bus</span><span class="sxs-lookup"><span data-stu-id="14762-155">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Recommended naming conventions for Azure resources]: ../guidance/guidance-naming-conventions.md
[Service Bus namespace with topic, subscription, and rule]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-subscription-rule/
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md

