---
title: "aaaCreate abonnement à une rubrique Service Bus de Azure et de la règle à l’aide du modèle Azure Resource Manager | Documents Microsoft"
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
ms.openlocfilehash: dbc46da8491aee4d0c73bd4db90c696008920df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-with-topic-subscription-and-rule-using-an-azure-resource-manager-template"></a><span data-ttu-id="7e993-103">Créer un espace de noms Service Bus avec rubrique, abonnement et règle à l’aide d’un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7e993-103">Create a Service Bus namespace with topic, subscription, and rule using an Azure Resource Manager template</span></span>

<span data-ttu-id="7e993-104">Cet article explique comment toouse un modèle Azure Resource Manager qui crée un espace de noms Service Bus avec une rubrique, un abonnement et une règle (filtre).</span><span class="sxs-lookup"><span data-stu-id="7e993-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace with a topic, subscription, and rule (filter).</span></span> <span data-ttu-id="7e993-105">Vous apprendrez comment toodefine les ressources qui sont déployés et comment les paramètres toodefine sont spécifiés lorsque le déploiement de hello est exécutée.</span><span class="sxs-lookup"><span data-stu-id="7e993-105">You learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="7e993-106">Vous pouvez utiliser ce modèle pour vos propres déploiements, ou personnaliser toomeet vos besoins</span><span class="sxs-lookup"><span data-stu-id="7e993-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="7e993-107">Pour en savoir plus sur la création de modèles, consultez [Création de modèles Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="7e993-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="7e993-108">Pour plus d’informations sur les pratiques et les modèles des conventions d’affectation de noms des ressources Azure, consultez [Conventions d’affectation de noms recommandées pour les ressources Azure][Recommended naming conventions for Azure resources].</span><span class="sxs-lookup"><span data-stu-id="7e993-108">For more information about practice and patterns on Azure resources naming conventions, see [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources].</span></span>

<span data-ttu-id="7e993-109">Pour le modèle complète de hello, consultez hello [espace de noms Service Bus avec la rubrique, abonnement et règle] [ Service Bus namespace with topic, subscription, and rule] modèle.</span><span class="sxs-lookup"><span data-stu-id="7e993-109">For hello complete template, see hello [Service Bus namespace with topic, subscription, and rule][Service Bus namespace with topic, subscription, and rule] template.</span></span>

> [!NOTE]
> <span data-ttu-id="7e993-110">Hello suivant modèles Azure Resource Manager est disponible pour le téléchargement et déploiement.</span><span class="sxs-lookup"><span data-stu-id="7e993-110">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="7e993-111">Créer un espace de noms Service Bus avec file d'attente et règle d’autorisation</span><span class="sxs-lookup"><span data-stu-id="7e993-111">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="7e993-112">Créer un espace de noms Service Bus avec file d’attente</span><span class="sxs-lookup"><span data-stu-id="7e993-112">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="7e993-113">Création d'un espace de noms Service Bus</span><span class="sxs-lookup"><span data-stu-id="7e993-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="7e993-114">Créer un espace de noms Service Bus par rubrique et abonnement</span><span class="sxs-lookup"><span data-stu-id="7e993-114">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> 
> <span data-ttu-id="7e993-115">toocheck pour les derniers modèles de hello, visitez hello [modèles de démarrage rapide Azure] [ Azure Quickstart Templates] la galerie et recherchez le Service Bus.</span><span class="sxs-lookup"><span data-stu-id="7e993-115">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="7e993-116">Qu'allez-vous déployer ?</span><span class="sxs-lookup"><span data-stu-id="7e993-116">What will you deploy?</span></span>

<span data-ttu-id="7e993-117">Avec ce modèle, vous déployez un espace de noms Service Bus avec rubrique, abonnement et règle (filtre).</span><span class="sxs-lookup"><span data-stu-id="7e993-117">With this template, you deploy a Service Bus namespace with topic, subscription, and rule (filter).</span></span>

<span data-ttu-id="7e993-118">Les [rubriques et les abonnements Service Bus](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) fournissent une forme de communication de type un-à-plusieurs dans un modèle de *publication/abonnement*.</span><span class="sxs-lookup"><span data-stu-id="7e993-118">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span> <span data-ttu-id="7e993-119">Lorsque vous utilisez les rubriques et les abonnements, les composants d’une application distribuée ne communiquent pas directement avec eux, au lieu de cela ils échangent des messages via la rubrique qui sert d’intermédiaire. Une rubrique de tooa abonnement ressemble à une file d’attente virtuelle qui reçoit des copies des messages qui ont été envoyés toohello rubrique.</span><span class="sxs-lookup"><span data-stu-id="7e993-119">When using topics and subscriptions, components of a distributed application do not communicate directly with each other, instead they exchange messages via topic that acts as an intermediary.A subscription tooa topic resembles a virtual queue that receives copies of messages that were sent toohello topic.</span></span> <span data-ttu-id="7e993-120">Un filtre d’abonnement vous permet de toospecify lesquelles messages envoyés tooa rubrique doit apparaître dans un abonnement à une rubrique spécifique.</span><span class="sxs-lookup"><span data-stu-id="7e993-120">A filter on subscription enables you toospecify which messages sent tooa topic should appear within a specific topic subscription.</span></span>

## <a name="what-are-rules-filters"></a><span data-ttu-id="7e993-121">Qu’est-ce qu’une règle (filtre) ?</span><span class="sxs-lookup"><span data-stu-id="7e993-121">What are rules (filters)?</span></span>

<span data-ttu-id="7e993-122">Dans de nombreux scénarios, les messages ayant des caractéristiques spécifiques doivent être traités différemment.</span><span class="sxs-lookup"><span data-stu-id="7e993-122">In many scenarios, messages that have specific characteristics must be processed in different ways.</span></span> <span data-ttu-id="7e993-123">tooenable, vous pouvez configurer les messages toofind abonnements qui ont des propriétés spécifiques, puis exécutez propriétés toothose de modifications.</span><span class="sxs-lookup"><span data-stu-id="7e993-123">tooenable this, you can configure subscriptions toofind messages that have specific properties and then perform modifications toothose properties.</span></span> <span data-ttu-id="7e993-124">Bien que les abonnements Service Bus consulter tous les messages envoyés toohello rubrique, vous pouvez copier uniquement un sous-ensemble de ces files d’attente de messages toohello virtuelle des abonnements.</span><span class="sxs-lookup"><span data-stu-id="7e993-124">Although Service Bus subscriptions see all messages sent toohello topic, you can only copy a subset of those messages toohello virtual subscription queue.</span></span> <span data-ttu-id="7e993-125">Pour ce faire, il faut utiliser des filtres d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="7e993-125">This is accomplished using subscription filters.</span></span> <span data-ttu-id="7e993-126">toolearn en savoir plus sur les règles (filtres), consultez [les règles et les actions](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span><span class="sxs-lookup"><span data-stu-id="7e993-126">toolearn more about rules (filters), see [Rules and actions](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span></span>

<span data-ttu-id="7e993-127">toorun hello déploiement automatiquement, cliquez sur hello suivant bouton :</span><span class="sxs-lookup"><span data-stu-id="7e993-127">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="7e993-128">[![Déployer tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="7e993-128">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="7e993-129">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7e993-129">Parameters</span></span>

<span data-ttu-id="7e993-130">Avec Azure Resource Manager, vous devez définir des paramètres pour les valeurs souhaitées toospecify lorsque le modèle de hello est déployé.</span><span class="sxs-lookup"><span data-stu-id="7e993-130">With Azure Resource Manager, you should define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="7e993-131">modèle de Hello inclut une section appelée `Parameters` qui contient toutes les valeurs de paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="7e993-131">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="7e993-132">Vous devez définir un paramètre pour les valeurs qui varient en fonction de projet que vous déployez hello ou dans l’environnement hello que vous effectuez le déploiement.</span><span class="sxs-lookup"><span data-stu-id="7e993-132">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="7e993-133">Ne définissez pas de paramètres pour les valeurs qui doivent restent hello identiques.</span><span class="sxs-lookup"><span data-stu-id="7e993-133">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="7e993-134">Chaque valeur de paramètre est utilisé dans hello modèle toodefine hello ressources qui sont déployés.</span><span class="sxs-lookup"><span data-stu-id="7e993-134">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="7e993-135">modèle de Hello définit hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="7e993-135">hello template defines hello following parameters:</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="7e993-136">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="7e993-136">serviceBusNamespaceName</span></span>
<span data-ttu-id="7e993-137">nom de Hello de toocreate d’espace de noms hello Service Bus.</span><span class="sxs-lookup"><span data-stu-id="7e993-137">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="7e993-138">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="7e993-138">serviceBusTopicName</span></span>
<span data-ttu-id="7e993-139">nom Hello de rubrique hello créée dans l’espace de noms Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="7e993-139">hello name of hello topic created in hello Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="7e993-140">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="7e993-140">serviceBusSubscriptionName</span></span>
<span data-ttu-id="7e993-141">nom Hello d’abonnement hello créé dans l’espace de noms Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="7e993-141">hello name of hello subscription created in hello Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```
### <a name="servicebusrulename"></a><span data-ttu-id="7e993-142">serviceBusRuleName</span><span class="sxs-lookup"><span data-stu-id="7e993-142">serviceBusRuleName</span></span>
<span data-ttu-id="7e993-143">nom de Hello de rule(filter) hello créé dans l’espace de noms Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="7e993-143">hello name of hello rule(filter) created in hello Service Bus namespace.</span></span>

```json
   "serviceBusRuleName": {
   "type": "string",
  }
```
### <a name="servicebusapiversion"></a><span data-ttu-id="7e993-144">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="7e993-144">serviceBusApiVersion</span></span>
<span data-ttu-id="7e993-145">version de l’API Service Bus Hello du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="7e993-145">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-toodeploy"></a><span data-ttu-id="7e993-146">Ressources toodeploy</span><span class="sxs-lookup"><span data-stu-id="7e993-146">Resources toodeploy</span></span>
<span data-ttu-id="7e993-147">Crée un espace de noms Service Bus standard de type **Messagerie**, avec rubrique, abonnement et règles.</span><span class="sxs-lookup"><span data-stu-id="7e993-147">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription and rules.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="7e993-148">Déploiement de toorun de commandes</span><span class="sxs-lookup"><span data-stu-id="7e993-148">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="7e993-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e993-149">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="7e993-150">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="7e993-150">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="7e993-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7e993-151">Next steps</span></span>
<span data-ttu-id="7e993-152">Maintenant que vous avez créé et déployé des ressources à l’aide du Gestionnaire de ressources Azure, découvrez comment toomanage ces ressources en consultant les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="7e993-152">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="7e993-153">Gérer Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="7e993-153">Manage Azure Service Bus</span></span>](service-bus-management-libraries.md)
* [<span data-ttu-id="7e993-154">Gestion de Service Bus avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e993-154">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="7e993-155">Gérer les ressources de Service Bus avec hello Explorateur Service Bus</span><span class="sxs-lookup"><span data-stu-id="7e993-155">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Recommended naming conventions for Azure resources]: ../guidance/guidance-naming-conventions.md
[Service Bus namespace with topic, subscription, and rule]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-subscription-rule/
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md

